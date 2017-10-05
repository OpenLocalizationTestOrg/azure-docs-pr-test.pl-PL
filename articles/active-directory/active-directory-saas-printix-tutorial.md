---
title: 'Samouczek: Integracji Azure Active Directory z Printix | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="6a8cb-103">Samouczek: Integracji Azure Active Directory z Printix</span><span class="sxs-lookup"><span data-stu-id="6a8cb-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="6a8cb-104">Z tego samouczka dowiesz się integrowanie Printix z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a8cb-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a8cb-105">Integracja z usługą Azure AD Printix zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a8cb-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Printix</span><span class="sxs-lookup"><span data-stu-id="6a8cb-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="6a8cb-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Printix (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a8cb-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a8cb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6a8cb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a8cb-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a8cb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a8cb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6a8cb-110">Prerequisites</span></span>

<span data-ttu-id="6a8cb-111">Aby skonfigurować integrację usługi Azure AD z Printix, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="6a8cb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a8cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a8cb-113">Printix logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6a8cb-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a8cb-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a8cb-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a8cb-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a8cb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a8cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a8cb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6a8cb-118">Scenario description</span></span>
<span data-ttu-id="6a8cb-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a8cb-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a8cb-121">Dodawanie Printix z galerii</span><span class="sxs-lookup"><span data-stu-id="6a8cb-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="6a8cb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6a8cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="6a8cb-123">Dodawanie Printix z galerii</span><span class="sxs-lookup"><span data-stu-id="6a8cb-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="6a8cb-124">Aby skonfigurować integrację usługi Azure AD Printix, należy dodać Printix z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a8cb-125">**Aby dodać Printix z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a8cb-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a8cb-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6a8cb-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a8cb-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6a8cb-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6a8cb-133">W polu wyszukiwania wpisz **Printix**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-133">In the search box, type **Printix**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="6a8cb-135">W panelu wyników wybierz **Printix**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a8cb-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6a8cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a8cb-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Printix w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a8cb-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Printix jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="6a8cb-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Printix musi się.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="6a8cb-141">W Printix, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a8cb-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Printix, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a8cb-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a8cb-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a8cb-145">**[Tworzenie użytkownika testowego Printix](#creating-a-printix-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Printix połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a8cb-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a8cb-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a8cb-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a8cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a8cb-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Printix.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="6a8cb-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Printix, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a8cb-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="6a8cb-151">W portalu Azure na **Printix** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6a8cb-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="6a8cb-155">Na **Printix domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="6a8cb-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="6a8cb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a8cb-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-158">The value is not real.</span></span> <span data-ttu-id="6a8cb-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="6a8cb-160">Skontaktuj się z [zespołem pomocy technicznej klienta Printix](mailto:support@printix.net) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="6a8cb-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="6a8cb-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a8cb-165">Logowanie do dzierżawy Printix jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="6a8cb-166">W menu u góry kliknij ikonę w prawym górnym rogu i wybierz pozycję "**uwierzytelniania**".</span><span class="sxs-lookup"><span data-stu-id="6a8cb-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="6a8cb-168">Na **Instalator** wybierz opcję **uwierzytelniania Włącz Azure/Office 365**</span><span class="sxs-lookup"><span data-stu-id="6a8cb-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="6a8cb-170">Na **Azure** karcie, wprowadź adres URL metadanych Federacji pole tekstowe z "**dokument metadanych usług federacyjnych**".</span><span class="sxs-lookup"><span data-stu-id="6a8cb-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="6a8cb-171">Dołącz plik xml metadanych, który został pobrany z usługi Azure AD do [zespołem pomocy technicznej Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="6a8cb-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="6a8cb-172">Następnie załaduj plik xml i wprowadzić adres URL metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="6a8cb-174">Kliknij przycisk "**Test**"przycisk i kliknij przycisk"**OK**" przycisku, jeśli test zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="6a8cb-175">Strona usługi Azure active directory zostaną wyświetlone po kliknięciu **test** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="6a8cb-176">"Powiodło się uruchomienie testu" poniżej oznacza, że po wprowadzeniu poświadczeń konta Azure testu, który będzie punktu obecności komunikat "Ustawienia sprawdzona". Następnie kliknij przycisk **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="6a8cb-178">Kliknij przycisk **zapisać** znajdującego się na "**uwierzytelniania**" strony.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="6a8cb-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6a8cb-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a8cb-180">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a8cb-181">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a8cb-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a8cb-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a8cb-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a8cb-183">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6a8cb-185">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a8cb-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a8cb-186">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a8cb-188">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a8cb-190">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a8cb-192">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6a8cb-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a8cb-194">a.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-194">a.</span></span> <span data-ttu-id="6a8cb-195">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a8cb-196">b.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-196">b.</span></span> <span data-ttu-id="6a8cb-197">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a8cb-198">c.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-198">c.</span></span> <span data-ttu-id="6a8cb-199">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a8cb-200">d.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-200">d.</span></span> <span data-ttu-id="6a8cb-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="6a8cb-202">Tworzenie użytkownika testowego Printix</span><span class="sxs-lookup"><span data-stu-id="6a8cb-202">Creating a Printix test user</span></span>

<span data-ttu-id="6a8cb-203">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Printix.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="6a8cb-204">Printix obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6a8cb-205">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-205">There is no action item for you in this section.</span></span> <span data-ttu-id="6a8cb-206">Nowy użytkownik został utworzony podczas próby dostępu Printix, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a8cb-207">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="6a8cb-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a8cb-208">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a8cb-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a8cb-209">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Printix.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6a8cb-211">**Aby przypisać Simona Britta Printix, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a8cb-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="6a8cb-212">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6a8cb-214">Na liście aplikacji zaznacz **Printix**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-214">In the applications list, select **Printix**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="6a8cb-216">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6a8cb-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-218">Click **Add** button.</span></span> <span data-ttu-id="6a8cb-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6a8cb-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a8cb-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a8cb-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a8cb-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a8cb-224">Testing single sign-on</span></span>

<span data-ttu-id="6a8cb-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a8cb-226">Po kliknięciu kafelka Printix w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Printix.</span><span class="sxs-lookup"><span data-stu-id="6a8cb-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a8cb-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6a8cb-227">Additional resources</span></span>

* [<span data-ttu-id="6a8cb-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a8cb-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a8cb-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a8cb-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

