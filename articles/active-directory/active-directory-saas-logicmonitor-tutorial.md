---
title: 'Samouczek: Integracji Azure Active Directory z LogicMonitor | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="8d6e2-103">Samouczek: Integracji Azure Active Directory z LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="8d6e2-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="8d6e2-104">Z tego samouczka dowiesz się integrowanie LogicMonitor z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d6e2-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d6e2-105">Integracja z usługą Azure AD LogicMonitor zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d6e2-106">Można kontrolować w usłudze Azure AD, który ma dostęp do LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="8d6e2-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="8d6e2-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do LogicMonitor (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e2-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d6e2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8d6e2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d6e2-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d6e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d6e2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8d6e2-110">Prerequisites</span></span>

<span data-ttu-id="8d6e2-111">Aby skonfigurować integrację usługi Azure AD z LogicMonitor, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="8d6e2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d6e2-113">LogicMonitor logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8d6e2-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d6e2-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d6e2-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d6e2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d6e2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d6e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d6e2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8d6e2-118">Scenario description</span></span>
<span data-ttu-id="8d6e2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d6e2-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d6e2-121">Dodawanie LogicMonitor z galerii</span><span class="sxs-lookup"><span data-stu-id="8d6e2-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="8d6e2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8d6e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="8d6e2-123">Dodawanie LogicMonitor z galerii</span><span class="sxs-lookup"><span data-stu-id="8d6e2-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="8d6e2-124">Aby skonfigurować integrację usługi Azure AD LogicMonitor, należy dodać LogicMonitor z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d6e2-125">**Aby dodać LogicMonitor z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8d6e2-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d6e2-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8d6e2-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d6e2-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8d6e2-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8d6e2-133">W polu wyszukiwania wpisz **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-133">In the search box, type **LogicMonitor**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="8d6e2-135">W panelu wyników wybierz **LogicMonitor**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d6e2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8d6e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d6e2-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LogicMonitor w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d6e2-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w LogicMonitor jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="8d6e2-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w LogicMonitor musi się.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="8d6e2-141">W LogicMonitor, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d6e2-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LogicMonitor, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d6e2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d6e2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d6e2-145">**[Tworzenie użytkownika testowego LogicMonitor](#creating-a-logicmonitor-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LogicMonitor połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d6e2-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d6e2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d6e2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8d6e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d6e2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="8d6e2-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LogicMonitor, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8d6e2-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="8d6e2-151">W portalu Azure na **LogicMonitor** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8d6e2-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="8d6e2-155">Na **LogicMonitor domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="8d6e2-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-157">a.</span></span> <span data-ttu-id="8d6e2-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="8d6e2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="8d6e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-159">b.</span></span> <span data-ttu-id="8d6e2-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="8d6e2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d6e2-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-161">These values are not real.</span></span> <span data-ttu-id="8d6e2-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8d6e2-163">Skontaktuj się z [zespołem pomocy technicznej klienta LogicMonitor](https://www.logicmonitor.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="8d6e2-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="8d6e2-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d6e2-168">Zaloguj się do Twojego **LogicMonitor** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="8d6e2-169">W menu u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="8d6e2-170">![Ustawienia](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8d6e2-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="8d6e2-171">W bat nawigacji po lewej stronie, kliknij przycisk **rejestracji jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="8d6e2-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="8d6e2-172">![Logowanie jednokrotne](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8d6e2-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="8d6e2-173">W **ustawień rejestracji jednokrotnej (SSO)** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="8d6e2-174">![Single Sign-On ustawienia](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8d6e2-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="8d6e2-175">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-175">a.</span></span> <span data-ttu-id="8d6e2-176">Wybierz **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="8d6e2-177">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-177">b.</span></span> <span data-ttu-id="8d6e2-178">Jako **domyślne przypisania roli**, wybierz pozycję **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="8d6e2-179">c.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-179">c.</span></span> <span data-ttu-id="8d6e2-180">Otwórz plik metadanych pobranych w programie Notatnik, a następnie wklej zawartość pliku do **metadanych dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="8d6e2-181">d.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-181">d.</span></span> <span data-ttu-id="8d6e2-182">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="8d6e2-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8d6e2-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d6e2-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d6e2-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d6e2-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d6e2-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e2-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d6e2-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8d6e2-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8d6e2-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d6e2-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d6e2-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d6e2-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d6e2-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d6e2-198">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-198">a.</span></span> <span data-ttu-id="8d6e2-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d6e2-200">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-200">b.</span></span> <span data-ttu-id="8d6e2-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d6e2-202">c.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-202">c.</span></span> <span data-ttu-id="8d6e2-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d6e2-204">d.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-204">d.</span></span> <span data-ttu-id="8d6e2-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="8d6e2-206">Tworzenie użytkownika testowego LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="8d6e2-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="8d6e2-207">Dla użytkowników usługi AAD można było zarejestrować musi być przygotowana do aplikacji LogicMonitor przy użyciu nazwy użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="8d6e2-208">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8d6e2-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="8d6e2-209">Zaloguj się do witryny firmy LogicMonitor jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="8d6e2-210">W menu u góry kliknij **ustawienia**, a następnie kliknij przycisk **ról i użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="8d6e2-211">![Role i użytkownicy](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "ról i użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8d6e2-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="8d6e2-212">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-212">Click **Add**.</span></span>

4. <span data-ttu-id="8d6e2-213">W **Dodaj konto** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8d6e2-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="8d6e2-214">![Dodaj konto](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Dodaj konto")</span><span class="sxs-lookup"><span data-stu-id="8d6e2-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="8d6e2-215">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-215">a.</span></span> <span data-ttu-id="8d6e2-216">Typ **Username**, **E-mail**, **hasło**, i **wpisz ponownie hasło** wartości użytkownika usługi Azure Active Directory ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="8d6e2-217">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-217">b.</span></span> <span data-ttu-id="8d6e2-218">Wybierz **ról**, **wyświetlić uprawnienia**i **stan**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="8d6e2-219">c.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-219">c.</span></span> <span data-ttu-id="8d6e2-220">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="8d6e2-221">Możesz użyć innych LogicMonitor użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez LogicMonitor do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d6e2-222">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e2-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d6e2-223">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8d6e2-225">**Aby przypisać Simona Britta LogicMonitor, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8d6e2-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="8d6e2-226">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8d6e2-228">Na liście aplikacji zaznacz **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="8d6e2-230">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8d6e2-232">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-232">Click **Add** button.</span></span> <span data-ttu-id="8d6e2-233">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8d6e2-235">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d6e2-236">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d6e2-237">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d6e2-238">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8d6e2-238">Testing single sign-on</span></span>

<span data-ttu-id="8d6e2-239">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="8d6e2-240">Po kliknięciu kafelka LogicMonitor w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="8d6e2-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="8d6e2-241">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d6e2-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8d6e2-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8d6e2-242">Additional resources</span></span>

* [<span data-ttu-id="8d6e2-243">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d6e2-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d6e2-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d6e2-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

