---
title: 'Samouczek: Integracji Azure Active Directory z Halosys | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać Halosys usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="8ecae-103">Samouczek: Integracji Azure Active Directory z Halosys</span><span class="sxs-lookup"><span data-stu-id="8ecae-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="8ecae-104">Z tego samouczka dowiesz się integrowanie Halosys z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ecae-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ecae-105">Integracja z usługą Azure AD Halosys zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ecae-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ecae-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Halosys</span><span class="sxs-lookup"><span data-stu-id="8ecae-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="8ecae-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Halosys (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ecae-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ecae-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8ecae-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8ecae-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ecae-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ecae-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ecae-110">Prerequisites</span></span>

<span data-ttu-id="8ecae-111">Aby skonfigurować integrację usługi Azure AD z Halosys, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ecae-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="8ecae-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ecae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ecae-113">Halosys jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8ecae-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="8ecae-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ecae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="8ecae-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ecae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ecae-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ecae-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8ecae-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ecae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="8ecae-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ecae-118">Scenario description</span></span>
<span data-ttu-id="8ecae-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ecae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="8ecae-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ecae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ecae-121">Dodawanie Halosys z galerii</span><span class="sxs-lookup"><span data-stu-id="8ecae-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="8ecae-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ecae-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="8ecae-123">Dodawanie Halosys z galerii</span><span class="sxs-lookup"><span data-stu-id="8ecae-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="8ecae-124">Aby skonfigurować integrację usługi Azure AD Halosys, należy dodać Halosys z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ecae-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ecae-125">**Aby dodać Halosys z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ecae-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ecae-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Usługa Active Directory][1]
2. <span data-ttu-id="8ecae-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="8ecae-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8ecae-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="8ecae-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Aplikacje][2]

4. <span data-ttu-id="8ecae-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="8ecae-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplikacje][3]

5. <span data-ttu-id="8ecae-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Aplikacje][4]

6. <span data-ttu-id="8ecae-135">W polu wyszukiwania wpisz **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-135">In the search box, type **Halosys**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="8ecae-137">W okienku wyników wybierz **Halosys**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8ecae-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ecae-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ecae-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ecae-140">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Halosys w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8ecae-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ecae-141">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Halosys jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ecae-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="8ecae-142">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Halosys musi się.</span><span class="sxs-lookup"><span data-stu-id="8ecae-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="8ecae-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Halosys.</span><span class="sxs-lookup"><span data-stu-id="8ecae-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="8ecae-144">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Halosys, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8ecae-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ecae-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ecae-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ecae-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ecae-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ecae-147">**[Tworzenie użytkownika testowego Halosys](#creating-a-halosys-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Halosys połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ecae-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8ecae-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ecae-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ecae-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8ecae-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ecae-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ecae-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ecae-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu i skonfigurować logowanie jednokrotne w aplikacji Halosys.</span><span class="sxs-lookup"><span data-stu-id="8ecae-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="8ecae-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Halosys, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ecae-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="8ecae-153">W klasycznym portalu na **Halosys** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ecae-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. <span data-ttu-id="8ecae-155">Na **jak chcesz użytkownikom zalogować się na Halosys** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="8ecae-157">Na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ecae-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="8ecae-159">a.</span><span class="sxs-lookup"><span data-stu-id="8ecae-159">a.</span></span> <span data-ttu-id="8ecae-160">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji Halosys przy użyciu następującego wzorca: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="8ecae-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="8ecae-161">b.In **adres URL identyfikatora** tekstowym, wpisz adres URL do następującego wzorca: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="8ecae-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="8ecae-162">Na **skonfigurować logowanie jednokrotne w Halosys** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik na komputerze:</span><span class="sxs-lookup"><span data-stu-id="8ecae-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="8ecae-164">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z zespołem pomocy technicznej Halosys i podaj z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="8ecae-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="8ecae-165">• Pobrany **pliku metadanych**</span><span class="sxs-lookup"><span data-stu-id="8ecae-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="8ecae-166">• **Adres URL logowania jednokrotnego SAML**</span><span class="sxs-lookup"><span data-stu-id="8ecae-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="8ecae-167">W klasycznym portalu, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD rejestracji jednokrotnej][10]

7. <span data-ttu-id="8ecae-169">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD rejestracji jednokrotnej][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ecae-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ecae-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ecae-172">W tej sekcji utworzysz użytkownika testowego w klasycznym portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ecae-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="8ecae-174">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ecae-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ecae-175">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="8ecae-177">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="8ecae-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8ecae-178">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ecae-180">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="8ecae-182">Na **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj następujące kroki: ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="8ecae-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="8ecae-183">a.</span><span class="sxs-lookup"><span data-stu-id="8ecae-183">a.</span></span> <span data-ttu-id="8ecae-184">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="8ecae-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="8ecae-185">b.</span><span class="sxs-lookup"><span data-stu-id="8ecae-185">b.</span></span> <span data-ttu-id="8ecae-186">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ecae-187">c.</span><span class="sxs-lookup"><span data-stu-id="8ecae-187">c.</span></span> <span data-ttu-id="8ecae-188">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-188">Click **Next**.</span></span>

6.  <span data-ttu-id="8ecae-189">Na **profilu użytkownika** okna dialogowego wykonaj następujące kroki: ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="8ecae-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="8ecae-190">a.</span><span class="sxs-lookup"><span data-stu-id="8ecae-190">a.</span></span> <span data-ttu-id="8ecae-191">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="8ecae-192">b.</span><span class="sxs-lookup"><span data-stu-id="8ecae-192">b.</span></span> <span data-ttu-id="8ecae-193">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="8ecae-194">c.</span><span class="sxs-lookup"><span data-stu-id="8ecae-194">c.</span></span> <span data-ttu-id="8ecae-195">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="8ecae-196">d.</span><span class="sxs-lookup"><span data-stu-id="8ecae-196">d.</span></span> <span data-ttu-id="8ecae-197">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="8ecae-198">e.</span><span class="sxs-lookup"><span data-stu-id="8ecae-198">e.</span></span> <span data-ttu-id="8ecae-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-199">Click **Next**.</span></span>

7. <span data-ttu-id="8ecae-200">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="8ecae-202">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ecae-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="8ecae-204">a.</span><span class="sxs-lookup"><span data-stu-id="8ecae-204">a.</span></span> <span data-ttu-id="8ecae-205">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="8ecae-206">b.</span><span class="sxs-lookup"><span data-stu-id="8ecae-206">b.</span></span> <span data-ttu-id="8ecae-207">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="8ecae-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="8ecae-208">Tworzenie użytkownika testowego Halosys</span><span class="sxs-lookup"><span data-stu-id="8ecae-208">Creating a Halosys test user</span></span>

<span data-ttu-id="8ecae-209">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Halosys.</span><span class="sxs-lookup"><span data-stu-id="8ecae-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="8ecae-210">Należy współpracować z zespołem pomocy technicznej Halosys Aby dodać użytkowników do platformy Halosys.</span><span class="sxs-lookup"><span data-stu-id="8ecae-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ecae-211">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ecae-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8ecae-212">W tej sekcji można włączyć Simona Britta do udostępnienia jej Halosys za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ecae-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8ecae-214">**Aby przypisać Simona Britta Halosys, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ecae-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="8ecae-215">W klasycznym portalu, aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="8ecae-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ecae-217">Na liście aplikacji zaznacz **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-217">In the applications list, select **Halosys**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="8ecae-219">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-219">In the menu on the top, click **Users**.</span></span>

    ![Przypisz użytkownika][203]

4. <span data-ttu-id="8ecae-221">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="8ecae-222">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="8ecae-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Przypisz użytkownika][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="8ecae-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ecae-224">Testing single sign-on</span></span>

<span data-ttu-id="8ecae-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ecae-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8ecae-226">Po kliknięciu kafelka Halosys w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Halosys.</span><span class="sxs-lookup"><span data-stu-id="8ecae-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8ecae-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ecae-227">Additional resources</span></span>

* [<span data-ttu-id="8ecae-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ecae-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ecae-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ecae-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
