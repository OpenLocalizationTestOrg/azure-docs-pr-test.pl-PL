---
title: "Samouczek: Integracji Azure Active Directory z SciQuest spędzają na katalog | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SciQuest spędzają na katalog."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="f0ce3-103">Samouczek: Integracji Azure Active Directory z SciQuest spędzają na katalog</span><span class="sxs-lookup"><span data-stu-id="f0ce3-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="f0ce3-104">Celem tego samouczka jest pokazanie sposobu integracji SciQuest spędzają na katalog w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0ce3-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="f0ce3-105">Integracja z usługą Azure AD SciQuest spędzają na katalog zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="f0ce3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do SciQuest spędzają na katalog</span><span class="sxs-lookup"><span data-stu-id="f0ce3-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="f0ce3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane SciQuest spędzają dyrektora (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0ce3-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f0ce3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f0ce3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f0ce3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0ce3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0ce3-110">Prerequisites</span></span>
<span data-ttu-id="f0ce3-111">Aby skonfigurować integrację usługi Azure AD z SciQuest spędzają na katalog, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="f0ce3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0ce3-112">An Azure AD subscription</span></span>
* <span data-ttu-id="f0ce3-113">Dyrektor spędzają SciQuest jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f0ce3-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0ce3-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="f0ce3-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f0ce3-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f0ce3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0ce3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="f0ce3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f0ce3-118">Scenario Description</span></span>
<span data-ttu-id="f0ce3-119">Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="f0ce3-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0ce3-121">Dodawanie SciQuest spędzają na katalog z galerii</span><span class="sxs-lookup"><span data-stu-id="f0ce3-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="f0ce3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f0ce3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="f0ce3-123">Dodawanie SciQuest spędzają na katalog z galerii</span><span class="sxs-lookup"><span data-stu-id="f0ce3-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="f0ce3-124">Aby skonfigurować integrację usługi Azure AD SciQuest spędzają na katalog, należy dodać SciQuest spędzają na katalog z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0ce3-125">**Aby dodać SciQuest spędzają na katalog z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f0ce3-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0ce3-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]

2. <span data-ttu-id="f0ce3-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f0ce3-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2]

4. <span data-ttu-id="f0ce3-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]

5. <span data-ttu-id="f0ce3-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4]

6. <span data-ttu-id="f0ce3-135">W polu wyszukiwania wpisz **sciQuest spędzają na katalog**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![Aplikacje][5]

7. <span data-ttu-id="f0ce3-137">W okienku wyników wybierz **SciQuest spędzają na katalog**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![Aplikacje][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0ce3-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f0ce3-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0ce3-140">Jest celem tej sekcji opisano, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SciQuest Dyrektor spędzają na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="f0ce3-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0ce3-141">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownika w SciQuest spędzają na katalog do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="f0ce3-142">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="f0ce3-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="f0ce3-144">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SciQuest spędzają na katalog, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0ce3-145">**[Konfigurowanie usługi Azure AD pojedynczego rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0ce3-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0ce3-147">**[Tworzenie użytkownika testowego SciQuest spędzają na katalog](#creating-a-halogen-software-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta spędzają na katalog SciQuest, połączonej z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f0ce3-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0ce3-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="f0ce3-150">Konfigurowanie usługi Azure AD pojedynczej rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f0ce3-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="f0ce3-151">Celem tej sekcji jest można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu Azure i skonfigurować logowanie jednokrotne w SciQuest spędzają na katalog aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="f0ce3-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SciQuest spędzają na katalog, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f0ce3-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="f0ce3-153">W klasycznym portalu Azure na **SciQuest spędzają na katalog** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne**  okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. <span data-ttu-id="f0ce3-155">Na **jak chcesz użytkownikom zalogować się na SciQuest spędzają na katalog** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][9]

3. <span data-ttu-id="f0ce3-157">Na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Konfiguruj ustawienia aplikacji][10]
   
     <span data-ttu-id="f0ce3-159">a.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-159">a.</span></span> <span data-ttu-id="f0ce3-160">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania się SciQuest spędzają na katalog aplikacji przy użyciu następującego wzorca: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="f0ce3-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="f0ce3-161">b.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-161">b.</span></span> <span data-ttu-id="f0ce3-162">W **adres URL odpowiedzi** pole tekstowe, należy wpisać taką samą wartość wpisana do **na adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="f0ce3-163">c.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-163">c.</span></span> <span data-ttu-id="f0ce3-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-164">Click **Next**.</span></span>

4. <span data-ttu-id="f0ce3-165">Na **skonfigurować logowanie jednokrotne w SciQuest spędzają na katalog** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![Co to jest program Azure AD Connect][11]

5. <span data-ttu-id="f0ce3-167">Skontaktuj się z pomocą SciQuest obsługuje Aby włączyć tę metodę uwierzytelniania przy użyciu metadanych pobranych powyżej.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="f0ce3-168">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![Co to jest program Azure AD Connect][15]

7. <span data-ttu-id="f0ce3-170">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0ce3-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0ce3-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0ce3-172">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="f0ce3-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f0ce3-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0ce3-174">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Co to jest program Azure AD Connect][100] 

2. <span data-ttu-id="f0ce3-176">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f0ce3-177">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Co to jest program Azure AD Connect][101] 

4. <span data-ttu-id="f0ce3-179">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Co to jest program Azure AD Connect][102] 

5. <span data-ttu-id="f0ce3-181">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Co to jest program Azure AD Connect][103] 
   
    <span data-ttu-id="f0ce3-183">a.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-183">a.</span></span> <span data-ttu-id="f0ce3-184">Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="f0ce3-185">b.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-185">b.</span></span> <span data-ttu-id="f0ce3-186">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="f0ce3-187">c.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-187">c.</span></span> <span data-ttu-id="f0ce3-188">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-188">Click **Next**.</span></span>

6. <span data-ttu-id="f0ce3-189">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Co to jest program Azure AD Connect][104] 
   
    <span data-ttu-id="f0ce3-191">a.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-191">a.</span></span> <span data-ttu-id="f0ce3-192">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="f0ce3-193">b.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-193">b.</span></span> <span data-ttu-id="f0ce3-194">W **nazwisko** txtbox, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="f0ce3-195">c.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-195">c.</span></span> <span data-ttu-id="f0ce3-196">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="f0ce3-197">d.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-197">d.</span></span> <span data-ttu-id="f0ce3-198">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="f0ce3-199">e.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-199">e.</span></span> <span data-ttu-id="f0ce3-200">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-200">Click **Next**.</span></span>

7. <span data-ttu-id="f0ce3-201">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Co to jest program Azure AD Connect][105]  

8. <span data-ttu-id="f0ce3-203">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f0ce3-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Co to jest program Azure AD Connect][106]   
   
    <span data-ttu-id="f0ce3-205">a.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-205">a.</span></span> <span data-ttu-id="f0ce3-206">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="f0ce3-207">b.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-207">b.</span></span> <span data-ttu-id="f0ce3-208">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="f0ce3-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="f0ce3-209">Tworzenie użytkownika testowego SciQuest spędzają na katalog</span><span class="sxs-lookup"><span data-stu-id="f0ce3-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="f0ce3-210">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="f0ce3-211">Należy skontaktować się z zespołem pomocy technicznej SciQuest spędzają na katalog i dostarczać szczegółowe informacje o Twoim koncie testu, aby został utworzony.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="f0ce3-212">Alternatywnie można też skorzystać w czasie inicjowania obsługi administracyjnej, pojedynczego logowania jednokrotnego funkcja, która jest obsługiwana przez SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="f0ce3-213">Po włączeniu w czasie inicjowania obsługi użytkowników są tworzone automatycznie przez SciQuest spędzają na katalog podczas jednego próba logowania jednokrotnego, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="f0ce3-214">Ta funkcja eliminuje potrzebę ręcznie utworzyć użytkowników odpowiednikiem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="f0ce3-215">Można uzyskać w czasie inicjowania obsługi administracyjnej włączone, musisz skontaktować się z korzystania z zespołem pomocy technicznej SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0ce3-216">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0ce3-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="f0ce3-217">Celem tej sekcji jest włączenie Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu jej SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![Co to jest program Azure AD Connect][200]

<span data-ttu-id="f0ce3-219">**Aby przypisać Simona Britta SciQuest spędzają na katalog, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f0ce3-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="f0ce3-220">W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Co to jest program Azure AD Connect][201]

2. <span data-ttu-id="f0ce3-222">Na liście aplikacji zaznacz **SciQuest spędzają na katalog**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Co to jest program Azure AD Connect][202]

3. <span data-ttu-id="f0ce3-224">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-224">In the menu on the top, click **Users**.</span></span>
   
    ![Co to jest program Azure AD Connect][203]

4. <span data-ttu-id="f0ce3-226">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![Co to jest program Azure AD Connect][204]

5. <span data-ttu-id="f0ce3-228">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Co to jest program Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="f0ce3-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f0ce3-230">Testing Single Sign-On</span></span>
<span data-ttu-id="f0ce3-231">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f0ce3-232">Po kliknięciu kafelka SciQuest spędzają na katalog, w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane SciQuest spędzają na katalog aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ce3-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0ce3-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f0ce3-233">Additional Resources</span></span>
* [<span data-ttu-id="f0ce3-234">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0ce3-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0ce3-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0ce3-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

