---
title: 'Samouczek: Integracji Azure Active Directory z PerformanceCentre | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e86adaf4bd9b4752f2aece8207a8a423ec5590a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="996fe-103">Samouczek: Integracji Azure Active Directory z PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="996fe-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="996fe-104">Z tego samouczka dowiesz się integrowanie PerformanceCentre z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="996fe-104">In this tutorial, you learn how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="996fe-105">Integracja z usługą Azure AD PerformanceCentre zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="996fe-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="996fe-106">Można kontrolować w usłudze Azure AD, który ma dostęp do PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="996fe-106">You can control in Azure AD who has access to PerformanceCentre</span></span>
- <span data-ttu-id="996fe-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do PerformanceCentre (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="996fe-107">You can enable your users to automatically get signed-on to PerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="996fe-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="996fe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="996fe-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="996fe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="996fe-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="996fe-110">Prerequisites</span></span>

<span data-ttu-id="996fe-111">Aby skonfigurować integrację usługi Azure AD z PerformanceCentre, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="996fe-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

- <span data-ttu-id="996fe-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="996fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="996fe-113">PerformanceCentre logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="996fe-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="996fe-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="996fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="996fe-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="996fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="996fe-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="996fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="996fe-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="996fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="996fe-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="996fe-118">Scenario description</span></span>
<span data-ttu-id="996fe-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="996fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="996fe-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="996fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="996fe-121">Dodawanie PerformanceCentre z galerii</span><span class="sxs-lookup"><span data-stu-id="996fe-121">Adding PerformanceCentre from the gallery</span></span>
2. <span data-ttu-id="996fe-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="996fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-the-gallery"></a><span data-ttu-id="996fe-123">Dodawanie PerformanceCentre z galerii</span><span class="sxs-lookup"><span data-stu-id="996fe-123">Adding PerformanceCentre from the gallery</span></span>
<span data-ttu-id="996fe-124">Aby skonfigurować integrację usługi Azure AD PerformanceCentre, należy dodać PerformanceCentre z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="996fe-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="996fe-125">**Aby dodać PerformanceCentre z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="996fe-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="996fe-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="996fe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="996fe-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="996fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="996fe-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="996fe-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="996fe-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="996fe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="996fe-133">W polu wyszukiwania wpisz **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="996fe-133">In the search box, type **PerformanceCentre**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="996fe-135">W panelu wyników wybierz **PerformanceCentre**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="996fe-135">In the results panel, select **PerformanceCentre**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="996fe-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="996fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="996fe-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PerformanceCentre w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="996fe-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="996fe-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w PerformanceCentre jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="996fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PerformanceCentre is to a user in Azure AD.</span></span> <span data-ttu-id="996fe-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w PerformanceCentre musi się.</span><span class="sxs-lookup"><span data-stu-id="996fe-140">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>

<span data-ttu-id="996fe-141">W PerformanceCentre, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="996fe-141">In PerformanceCentre, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="996fe-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PerformanceCentre, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="996fe-142">To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="996fe-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="996fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="996fe-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="996fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="996fe-145">**[Tworzenie użytkownika testowego PerformanceCentre](#creating-a-performancecentre-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta PerformanceCentre połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="996fe-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="996fe-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="996fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="996fe-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="996fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="996fe-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="996fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="996fe-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="996fe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="996fe-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z PerformanceCentre, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="996fe-150">**To configure Azure AD single sign-on with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="996fe-151">W portalu Azure na **PerformanceCentre** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="996fe-151">In the Azure portal, on the **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="996fe-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="996fe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="996fe-155">Na **PerformanceCentre domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="996fe-155">On the **PerformanceCentre Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="996fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="996fe-157">a.</span></span> <span data-ttu-id="996fe-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="996fe-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="996fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="996fe-159">b.</span></span> <span data-ttu-id="996fe-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="996fe-160">In the **Identifier** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="996fe-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="996fe-161">These values are not real.</span></span> <span data-ttu-id="996fe-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="996fe-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="996fe-163">Skontaktuj się z [zespołem pomocy technicznej klienta PerformanceCentre](https://www.performancecentre.com/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="996fe-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="996fe-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="996fe-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="996fe-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="996fe-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="996fe-168">Na **konfiguracji PerformanceCentre** , kliknij przycisk **skonfigurować PerformanceCentre** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="996fe-168">On the **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** to open **Configure sign-on** window.</span></span> <span data-ttu-id="996fe-169">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="996fe-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="996fe-171">Logowanie do Twojej **PerformanceCentre** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="996fe-171">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="996fe-172">Na karcie po lewej stronie kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="996fe-172">In the tab on the left side, click **Configure**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][10]

9. <span data-ttu-id="996fe-174">Na karcie po lewej stronie kliknij **różne**, a następnie kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="996fe-174">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][11]

10. <span data-ttu-id="996fe-176">Jako **protokołu**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="996fe-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][12]

11. <span data-ttu-id="996fe-178">Otwórz w Notatniku plik metadanych pobranych, skopiuj zawartość, wklej ją do **metadanych dostawcy tożsamości** pola tekstowego, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="996fe-178">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][13]

12. <span data-ttu-id="996fe-180">Sprawdź, czy wartości **jednostki podstawowego adresu URL** i **adres URL Identyfikatora jednostki** są poprawne.</span><span class="sxs-lookup"><span data-stu-id="996fe-180">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD rejestracji jednokrotnej][14]

> [!TIP]
> <span data-ttu-id="996fe-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="996fe-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="996fe-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="996fe-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="996fe-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="996fe-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="996fe-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="996fe-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="996fe-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="996fe-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="996fe-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="996fe-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="996fe-189">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="996fe-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="996fe-191">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="996fe-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="996fe-193">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="996fe-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="996fe-195">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="996fe-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="996fe-197">a.</span><span class="sxs-lookup"><span data-stu-id="996fe-197">a.</span></span> <span data-ttu-id="996fe-198">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="996fe-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="996fe-199">b.</span><span class="sxs-lookup"><span data-stu-id="996fe-199">b.</span></span> <span data-ttu-id="996fe-200">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="996fe-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="996fe-201">c.</span><span class="sxs-lookup"><span data-stu-id="996fe-201">c.</span></span> <span data-ttu-id="996fe-202">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="996fe-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="996fe-203">d.</span><span class="sxs-lookup"><span data-stu-id="996fe-203">d.</span></span> <span data-ttu-id="996fe-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="996fe-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="996fe-205">Tworzenie użytkownika testowego PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="996fe-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="996fe-206">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="996fe-206">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="996fe-207">**Aby utworzyć użytkownika o nazwie Simona Britta w PerformanceCentre, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="996fe-207">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="996fe-208">Logowanie się do witryny firmy PerformanceCentre jako administrator.</span><span class="sxs-lookup"><span data-stu-id="996fe-208">Sign on to your PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="996fe-209">W menu po lewej stronie kliknij **Interrelate**, a następnie kliknij przycisk **utworzyć uczestnika**.</span><span class="sxs-lookup"><span data-stu-id="996fe-209">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Utwórz użytkownika][400]

3. <span data-ttu-id="996fe-211">Na **Interrelate — tworzenie uczestnika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="996fe-211">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![Utwórz użytkownika][401]
    
    <span data-ttu-id="996fe-213">a.</span><span class="sxs-lookup"><span data-stu-id="996fe-213">a.</span></span> <span data-ttu-id="996fe-214">Wpisz wymagane atrybuty Simona Britta do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="996fe-214">Type the required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="996fe-215">Atrybut nazwy użytkownika w Britta w PerformanceCentre musi być taka sama jak nazwa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="996fe-215">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    
    <span data-ttu-id="996fe-216">b.</span><span class="sxs-lookup"><span data-stu-id="996fe-216">b.</span></span> <span data-ttu-id="996fe-217">Wybierz **Administrator klienta** jako **wybierz rolę**.</span><span class="sxs-lookup"><span data-stu-id="996fe-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="996fe-218">c.</span><span class="sxs-lookup"><span data-stu-id="996fe-218">c.</span></span> <span data-ttu-id="996fe-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="996fe-219">Click **Save**.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="996fe-220">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="996fe-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="996fe-221">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="996fe-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PerformanceCentre.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="996fe-223">**Aby przypisać Simona Britta PerformanceCentre, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="996fe-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="996fe-224">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="996fe-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="996fe-226">Na liście aplikacji zaznacz **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="996fe-226">In the applications list, select **PerformanceCentre**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="996fe-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="996fe-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="996fe-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="996fe-230">Click **Add** button.</span></span> <span data-ttu-id="996fe-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="996fe-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="996fe-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="996fe-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="996fe-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="996fe-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="996fe-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="996fe-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="996fe-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="996fe-236">Testing single sign-on</span></span>

<span data-ttu-id="996fe-237">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="996fe-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="996fe-238">Po kliknięciu kafelka PerformanceCentre w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="996fe-238">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="996fe-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="996fe-239">Additional resources</span></span>

* [<span data-ttu-id="996fe-240">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="996fe-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="996fe-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="996fe-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

