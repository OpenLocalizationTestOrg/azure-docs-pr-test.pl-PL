---
title: 'Samouczek: Integracji Azure Active Directory z Neota logiki Studio | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Neota logiki Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="20b02-103">Samouczek: Integracji Azure Active Directory z Neota logiki Studio</span><span class="sxs-lookup"><span data-stu-id="20b02-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="20b02-104">Z tego samouczka dowiesz się integrowanie Neota Studio logiki w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20b02-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20b02-105">Integracja z usługą Azure AD Neota logiki Studio zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="20b02-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="20b02-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Neota logiki Studio</span><span class="sxs-lookup"><span data-stu-id="20b02-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="20b02-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Studio logiki Neota (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20b02-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20b02-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="20b02-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="20b02-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="20b02-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="20b02-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20b02-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20b02-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="20b02-111">Prerequisites</span></span>

<span data-ttu-id="20b02-112">Aby skonfigurować integrację usługi Azure AD z Neota Studio logiki, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="20b02-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="20b02-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20b02-113">An Azure AD subscription</span></span>
- <span data-ttu-id="20b02-114">Neota logiki Studio jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="20b02-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20b02-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="20b02-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20b02-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="20b02-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20b02-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="20b02-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20b02-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20b02-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20b02-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="20b02-119">Scenario description</span></span>

<span data-ttu-id="20b02-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="20b02-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20b02-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="20b02-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20b02-122">Dodawanie Studio logiki Neota z galerii</span><span class="sxs-lookup"><span data-stu-id="20b02-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="20b02-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="20b02-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="20b02-124">Dodawanie Studio logiki Neota z galerii</span><span class="sxs-lookup"><span data-stu-id="20b02-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="20b02-125">Aby skonfigurować integrację Neota Studio logiki w usłudze Azure Active Directory, należy dodać Studio logiki Neota z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="20b02-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="20b02-126">**Aby dodać Studio logiki Neota z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="20b02-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="20b02-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="20b02-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="20b02-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="20b02-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="20b02-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="20b02-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="20b02-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20b02-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="20b02-134">W polu wyszukiwania wpisz **Studio logiki Neota**.</span><span class="sxs-lookup"><span data-stu-id="20b02-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="20b02-136">W panelu wyników wybierz **Studio logiki Neota**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="20b02-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20b02-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="20b02-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="20b02-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Studio logiki Neota oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="20b02-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="20b02-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Studio logiki Neota jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20b02-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="20b02-141">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Studio logiki Neota musi się.</span><span class="sxs-lookup"><span data-stu-id="20b02-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="20b02-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Studio logiki Neota.</span><span class="sxs-lookup"><span data-stu-id="20b02-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="20b02-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Studio logiki Neota, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="20b02-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="20b02-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="20b02-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="20b02-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="20b02-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20b02-146">**[Tworzenie użytkownika testowego Studio logiki Neota](#creating-a-neota-logic-studio-test-user)**  — aby odpowiednikiem Simona Britta w Studio logiki Neota, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20b02-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="20b02-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="20b02-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20b02-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="20b02-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20b02-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="20b02-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20b02-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Neota logiki Studio.</span><span class="sxs-lookup"><span data-stu-id="20b02-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="20b02-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Studio logiki Neota, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="20b02-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="20b02-152">W portalu Azure na **Studio logiki Neota** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="20b02-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="20b02-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="20b02-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="20b02-156">Na **Neota logiki Studio domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20b02-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="20b02-158">a.</span><span class="sxs-lookup"><span data-stu-id="20b02-158">a.</span></span> <span data-ttu-id="20b02-159">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="20b02-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="20b02-160">b.</span><span class="sxs-lookup"><span data-stu-id="20b02-160">b.</span></span> <span data-ttu-id="20b02-161">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="20b02-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20b02-162">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="20b02-162">These values are not the real.</span></span> <span data-ttu-id="20b02-163">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="20b02-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="20b02-164">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="20b02-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="20b02-165">Skontaktuj się z [zespołem pomocy technicznej klienta Studio logiki Neota](https://www.neotalogic.com/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="20b02-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="20b02-166">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="20b02-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="20b02-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20b02-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20b02-170">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [Studio logiki Neota pomocy technicznej](https://www.neotalogic.com/contact-us/) zespołu i zapewnić ich z pobrane **XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="20b02-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="20b02-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="20b02-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="20b02-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="20b02-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="20b02-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20b02-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20b02-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20b02-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="20b02-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="20b02-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="20b02-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="20b02-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="20b02-178">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="20b02-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20b02-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="20b02-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20b02-182">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20b02-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20b02-184">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20b02-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20b02-186">a.</span><span class="sxs-lookup"><span data-stu-id="20b02-186">a.</span></span> <span data-ttu-id="20b02-187">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20b02-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20b02-188">b.</span><span class="sxs-lookup"><span data-stu-id="20b02-188">b.</span></span> <span data-ttu-id="20b02-189">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="20b02-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20b02-190">c.</span><span class="sxs-lookup"><span data-stu-id="20b02-190">c.</span></span> <span data-ttu-id="20b02-191">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="20b02-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="20b02-192">d.</span><span class="sxs-lookup"><span data-stu-id="20b02-192">d.</span></span> <span data-ttu-id="20b02-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="20b02-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="20b02-194">Tworzenie użytkownika testowego Neota logiki Studio</span><span class="sxs-lookup"><span data-stu-id="20b02-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="20b02-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Studio logiki Neota.</span><span class="sxs-lookup"><span data-stu-id="20b02-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="20b02-196">Korzystanie z [zespołem pomocy technicznej klienta Studio logiki Neota](https://www.neotalogic.com/contact-us/) Aby dodać użytkowników na platformie Neota logiki Studio.</span><span class="sxs-lookup"><span data-stu-id="20b02-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="20b02-197">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="20b02-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="20b02-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20b02-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="20b02-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Neota logiki Studio.</span><span class="sxs-lookup"><span data-stu-id="20b02-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="20b02-201">**Aby przypisać Simona Britta Studio logiki Neota, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="20b02-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="20b02-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="20b02-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="20b02-204">Na liście aplikacji zaznacz **Studio logiki Neota**.</span><span class="sxs-lookup"><span data-stu-id="20b02-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="20b02-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="20b02-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="20b02-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20b02-208">Click **Add** button.</span></span> <span data-ttu-id="20b02-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20b02-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="20b02-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="20b02-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="20b02-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20b02-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20b02-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20b02-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20b02-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="20b02-214">Testing single sign-on</span></span>

<span data-ttu-id="20b02-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="20b02-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="20b02-216">Kliknij Kafelek Studio logiki Neota w panelu dostępu, nastąpi przekierowanie do strony logowania organizacji.</span><span class="sxs-lookup"><span data-stu-id="20b02-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="20b02-217">Po pomyślnego logowania użytkownik będzie można zalogowane Neota Studio logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20b02-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="20b02-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="20b02-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="20b02-219">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="20b02-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="20b02-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="20b02-220">Additional resources</span></span>

* [<span data-ttu-id="20b02-221">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20b02-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20b02-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="20b02-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

