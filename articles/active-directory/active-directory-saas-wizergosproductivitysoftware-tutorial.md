---
title: 'Samouczek: Integracji Azure Active Directory z Wizergos oprogramowanie | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Wizergos wydajności oprogramowania."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="4562f-103">Samouczek: Integracji Azure Active Directory z Wizergos wydajności oprogramowania</span><span class="sxs-lookup"><span data-stu-id="4562f-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="4562f-104">Celem tego samouczka jest pokazanie sposobu integracji Wizergos wydajności oprogramowania z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4562f-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4562f-105">Integrowanie Wizergos wydajności oprogramowania z usługi Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4562f-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4562f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Wizergos wydajności oprogramowania</span><span class="sxs-lookup"><span data-stu-id="4562f-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="4562f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Wizergos oprogramowanie rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4562f-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="4562f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4562f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4562f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4562f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4562f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4562f-110">Prerequisites</span></span>
<span data-ttu-id="4562f-111">Aby skonfigurować integrację usługi Azure AD z oprogramowaniem wydajność Wizergos, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4562f-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="4562f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4562f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4562f-113">Subskrypcja Wizergos wydajności oprogramowania logowanie Jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="4562f-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="4562f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4562f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="4562f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4562f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4562f-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4562f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4562f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4562f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4562f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4562f-118">Scenario description</span></span>
<span data-ttu-id="4562f-119">Celem tego samouczka jest umożliwienie test rejestracji Jednokrotnej programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4562f-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="4562f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4562f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4562f-121">Dodawanie Wizergos oprogramowanie z galerii</span><span class="sxs-lookup"><span data-stu-id="4562f-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="4562f-122">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="4562f-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="4562f-123">Dodawanie Wizergos oprogramowanie z galerii</span><span class="sxs-lookup"><span data-stu-id="4562f-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="4562f-124">Aby skonfigurować integrację usługi Azure AD Wizergos oprogramowanie, należy dodać Wizergos oprogramowanie z poziomu galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4562f-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4562f-125">**Aby dodać Wizergos oprogramowanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4562f-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4562f-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4562f-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]
2. <span data-ttu-id="4562f-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="4562f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4562f-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="4562f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2]
4. <span data-ttu-id="4562f-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="4562f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="4562f-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="4562f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4]
6. <span data-ttu-id="4562f-135">W polu wyszukiwania wpisz **Wizergos oprogramowanie**.</span><span class="sxs-lookup"><span data-stu-id="4562f-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="4562f-137">W panelu wyników wybierz **Wizergos oprogramowanie**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4562f-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Wybieranie aplikacji w galerii](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="4562f-139">Konfiguracja i testowanie logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="4562f-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="4562f-140">Jest celem tej sekcji opisano, jak skonfigurować i przetestować Azure AD SSO z Wizergos wydajności oprogramowania w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4562f-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4562f-141">Dla logowania jednokrotnego do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownika w Wizergos oprogramowanie do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4562f-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="4562f-142">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="4562f-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="4562f-144">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z BynWizergos Softwareder wydajności, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="4562f-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4562f-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4562f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4562f-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4562f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4562f-147">**[Tworzenie użytkownika testowego oprogramowanie Wizergos](#creating-a-wizergos-productivity-software-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Wizergos wydajności oprogramowania, które jest połączone z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4562f-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4562f-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4562f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4562f-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="4562f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="4562f-150">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="4562f-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="4562f-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu i skonfigurować logowanie jednokrotne w aplikacji Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="4562f-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Wizergos oprogramowanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4562f-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="4562f-153">W klasycznym portalu na **Wizergos oprogramowanie** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4562f-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. <span data-ttu-id="4562f-155">Na **jak chcesz użytkownikom zalogować się na oprogramowanie Wizergos** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="4562f-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="4562f-157">Na **Konfigurowanie ustawień aplikacji** strony okna dialogowego, kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="4562f-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="4562f-159">Na **skonfigurować logowanie jednokrotne w oprogramowanie Wizergos** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik na komputerze:</span><span class="sxs-lookup"><span data-stu-id="4562f-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="4562f-161">W oknie przeglądarki innej witryny sieci web logowanie do dzierżawy Wizergos wydajności oprogramowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4562f-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="4562f-162">Wybierz z hamburger menu **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4562f-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="4562f-164">Na stronie Administracja w menu po lewej stronie wybierz **uwierzytelniania** i wybierz polecenie **usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="4562f-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="4562f-166">Wykonaj następujące czynności na **uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4562f-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="4562f-168">Kliknij przycisk **przekazać** przycisk, aby przekazać certyfikat pobrany z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4562f-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="4562f-169">W **adres URL wystawcy** pole tekstowe umieścić wartość elementu **adres URL wystawcy** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4562f-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="4562f-170">W **URL rejestracji jednokrotnej** pole tekstowe umieścić wartość elementu **pojedynczy znak na adres URL usługi** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4562f-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="4562f-171">W **pojedynczego adresu URL Sign-Out** pole tekstowe umieścić wartość elementu **pojedynczy adres URL usługi Sign-out** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4562f-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="4562f-172">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4562f-172">Click **Save** button.</span></span>
9. <span data-ttu-id="4562f-173">W klasycznym portalu, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4562f-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][10]
10. <span data-ttu-id="4562f-175">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4562f-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4562f-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4562f-177">Create an Azure AD test user</span></span>
<span data-ttu-id="4562f-178">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4562f-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="4562f-180">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4562f-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4562f-181">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4562f-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="4562f-183">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="4562f-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4562f-184">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4562f-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="4562f-186">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4562f-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="4562f-188">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4562f-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="4562f-190">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="4562f-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="4562f-191">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4562f-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="4562f-192">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="4562f-192">Click **Next**.</span></span>
6. <span data-ttu-id="4562f-193">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4562f-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="4562f-195">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4562f-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="4562f-196">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="4562f-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="4562f-197">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="4562f-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="4562f-198">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4562f-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="4562f-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="4562f-199">Click **Next**.</span></span>
7. <span data-ttu-id="4562f-200">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="4562f-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="4562f-202">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4562f-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="4562f-204">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="4562f-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="4562f-205">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="4562f-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="4562f-206">Tworzenie użytkownika testowego Wizergos wydajności oprogramowania</span><span class="sxs-lookup"><span data-stu-id="4562f-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="4562f-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="4562f-208">Proszę współpracować z zespołem pomocy technicznej Wizergos wydajności oprogramowania za pomocą [ support@wizergos.com ](emailTo:support@wizergos.com) Aby dodać użytkowników na platformie Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4562f-209">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4562f-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="4562f-210">Celem tej sekcji jest włączenie Simona Britta się za pomocą logowania jednokrotnego Azure przez udostępnienie jej do Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Przypisz użytkownika][200]

<span data-ttu-id="4562f-212">**Aby przypisać Simona Britta Wizergos oprogramowanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4562f-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="4562f-213">W klasycznym portalu, aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="4562f-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Przypisz użytkownika][201]
2. <span data-ttu-id="4562f-215">Na liście aplikacji zaznacz **Wizergos oprogramowanie**.</span><span class="sxs-lookup"><span data-stu-id="4562f-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="4562f-217">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4562f-217">In the menu on the top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203]
4. <span data-ttu-id="4562f-219">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="4562f-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="4562f-220">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="4562f-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="4562f-222">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4562f-222">Test single sign-on</span></span>
<span data-ttu-id="4562f-223">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4562f-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4562f-224">Po kliknięciu kafelka Wizergos oprogramowanie w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="4562f-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4562f-225">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4562f-225">Additional resources</span></span>
* [<span data-ttu-id="4562f-226">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4562f-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4562f-227">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4562f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
