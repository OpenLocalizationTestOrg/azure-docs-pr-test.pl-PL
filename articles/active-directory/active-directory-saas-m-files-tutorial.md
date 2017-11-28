---
title: 'Samouczek: Integracji Azure Active Directory z plikami M | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i pliki M."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="56e58-103">Samouczek: Integracji Azure Active Directory z plikami M</span><span class="sxs-lookup"><span data-stu-id="56e58-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="56e58-104">Z tego samouczka dowiesz się integrowanie M plików w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56e58-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56e58-105">Integrowanie M pliki z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="56e58-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56e58-106">Można kontrolować w usłudze Azure AD, który ma dostęp do plików M</span><span class="sxs-lookup"><span data-stu-id="56e58-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="56e58-107">Umożliwia użytkownikom automatycznie pobrać zalogowane M — pliki (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56e58-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56e58-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="56e58-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56e58-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56e58-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56e58-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="56e58-110">Prerequisites</span></span>

<span data-ttu-id="56e58-111">Aby skonfigurować integrację usługi Azure AD z plikami M, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="56e58-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="56e58-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56e58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56e58-113">Pliki M logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="56e58-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56e58-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="56e58-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56e58-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="56e58-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56e58-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="56e58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56e58-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56e58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56e58-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="56e58-118">Scenario description</span></span>
<span data-ttu-id="56e58-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="56e58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56e58-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="56e58-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56e58-121">Trwa dodawanie plików M z galerii</span><span class="sxs-lookup"><span data-stu-id="56e58-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="56e58-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="56e58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="56e58-123">Trwa dodawanie plików M z galerii</span><span class="sxs-lookup"><span data-stu-id="56e58-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="56e58-124">Aby skonfigurować integrację usługi Azure AD M plików, należy dodać pliki M z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="56e58-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56e58-125">**Aby dodać pliki M z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="56e58-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56e58-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="56e58-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="56e58-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="56e58-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56e58-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="56e58-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="56e58-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56e58-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="56e58-133">W polu wyszukiwania wpisz **pliki M**.</span><span class="sxs-lookup"><span data-stu-id="56e58-133">In the search box, type **M-Files**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="56e58-135">W panelu wyników wybierz **M pliki**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="56e58-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56e58-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="56e58-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56e58-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z plikami M, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="56e58-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56e58-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w plikach M jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56e58-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="56e58-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w plikach M.</span><span class="sxs-lookup"><span data-stu-id="56e58-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="56e58-141">W plikach M, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="56e58-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56e58-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z plikami M, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="56e58-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56e58-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="56e58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56e58-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="56e58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56e58-145">**[Tworzenie użytkownika testowego pliki M](#creating-a-m-files-test-user)**  — aby odpowiednikiem Britta Simona w plikach M jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="56e58-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="56e58-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="56e58-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56e58-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="56e58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56e58-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="56e58-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56e58-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji M plików.</span><span class="sxs-lookup"><span data-stu-id="56e58-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="56e58-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z plikami M, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="56e58-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="56e58-151">W portalu Azure na **M pliki** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="56e58-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="56e58-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="56e58-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="56e58-155">Na **adresy URL i pliki M domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="56e58-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="56e58-157">a.</span><span class="sxs-lookup"><span data-stu-id="56e58-157">a.</span></span> <span data-ttu-id="56e58-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="56e58-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="56e58-159">b.</span><span class="sxs-lookup"><span data-stu-id="56e58-159">b.</span></span> <span data-ttu-id="56e58-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="56e58-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56e58-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="56e58-161">These values are not real.</span></span> <span data-ttu-id="56e58-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="56e58-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="56e58-163">Skontaktuj się z [zespołem pomocy technicznej klienta pliki M](mailto:support@m-files.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="56e58-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="56e58-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="56e58-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="56e58-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="56e58-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="56e58-168">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołu obsługi plików M](mailto:support@m-files.com) i podaj metadanych pobranych.</span><span class="sxs-lookup"><span data-stu-id="56e58-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="56e58-169">Wykonaj poniższe czynności, jeśli chcesz skonfigurować logowanie Jednokrotne dla Ciebie M pliku aplikacji komputerowych.</span><span class="sxs-lookup"><span data-stu-id="56e58-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="56e58-170">Żadne dodatkowe czynności nie są wymagane, jeśli chcesz skonfigurować logowania jednokrotnego dla wersji web M plików.</span><span class="sxs-lookup"><span data-stu-id="56e58-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="56e58-171">Wykonaj poniższe czynności, aby skonfigurować aplikację pulpitu pliku M do włączenia funkcji logowania jednokrotnego w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56e58-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="56e58-172">Aby pobrać pliki M, przejdź do [pobrać pliki M](https://www.m-files.com/en/download-latest-version) strony.</span><span class="sxs-lookup"><span data-stu-id="56e58-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="56e58-173">Otwórz **ustawienia pulpitu pliki M** okna.</span><span class="sxs-lookup"><span data-stu-id="56e58-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="56e58-174">Następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="56e58-174">Then, click **Add**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="56e58-176">Na **właściwości połączenia magazynu dokumentu** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="56e58-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="56e58-178">W obszarze serwera, sekcja typu wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="56e58-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="56e58-179">a.</span><span class="sxs-lookup"><span data-stu-id="56e58-179">a.</span></span> <span data-ttu-id="56e58-180">Aby uzyskać **nazwa**, typ `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="56e58-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="56e58-181">b.</span><span class="sxs-lookup"><span data-stu-id="56e58-181">b.</span></span> <span data-ttu-id="56e58-182">Aby uzyskać **numer portu**, typ **4466**.</span><span class="sxs-lookup"><span data-stu-id="56e58-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="56e58-183">c.</span><span class="sxs-lookup"><span data-stu-id="56e58-183">c.</span></span> <span data-ttu-id="56e58-184">Aby uzyskać **protokołu**, wybierz pozycję **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="56e58-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="56e58-185">d.</span><span class="sxs-lookup"><span data-stu-id="56e58-185">d.</span></span> <span data-ttu-id="56e58-186">W **uwierzytelniania** pól, zaznacz **określonego użytkownika systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="56e58-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="56e58-187">Następnie zostanie wyświetlony monit o strony podpisywania.</span><span class="sxs-lookup"><span data-stu-id="56e58-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="56e58-188">Wstaw poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56e58-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="56e58-189">e.</span><span class="sxs-lookup"><span data-stu-id="56e58-189">e.</span></span> <span data-ttu-id="56e58-190">Aby uzyskać **magazynu na serwerze**, wybierz odpowiedni magazyn na serwerze.</span><span class="sxs-lookup"><span data-stu-id="56e58-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="56e58-191">f.</span><span class="sxs-lookup"><span data-stu-id="56e58-191">f.</span></span> <span data-ttu-id="56e58-192">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="56e58-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="56e58-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="56e58-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56e58-194">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="56e58-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56e58-195">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56e58-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56e58-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56e58-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="56e58-197">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="56e58-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="56e58-199">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="56e58-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56e58-200">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="56e58-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56e58-202">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="56e58-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56e58-204">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56e58-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56e58-206">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="56e58-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56e58-208">a.</span><span class="sxs-lookup"><span data-stu-id="56e58-208">a.</span></span> <span data-ttu-id="56e58-209">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56e58-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56e58-210">b.</span><span class="sxs-lookup"><span data-stu-id="56e58-210">b.</span></span> <span data-ttu-id="56e58-211">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56e58-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56e58-212">c.</span><span class="sxs-lookup"><span data-stu-id="56e58-212">c.</span></span> <span data-ttu-id="56e58-213">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="56e58-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56e58-214">d.</span><span class="sxs-lookup"><span data-stu-id="56e58-214">d.</span></span> <span data-ttu-id="56e58-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="56e58-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="56e58-216">Tworzenie użytkownika testowego M — pliki</span><span class="sxs-lookup"><span data-stu-id="56e58-216">Creating a M-Files test user</span></span>

<span data-ttu-id="56e58-217">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w plikach M.</span><span class="sxs-lookup"><span data-stu-id="56e58-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="56e58-218">Praca z [zespołu obsługi plików M](mailto:support@m-files.com) Aby dodać użytkowników w plikach M.</span><span class="sxs-lookup"><span data-stu-id="56e58-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56e58-219">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56e58-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="56e58-220">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do plików M.</span><span class="sxs-lookup"><span data-stu-id="56e58-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="56e58-222">**Aby przypisać Simona Britta M pliki, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="56e58-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="56e58-223">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="56e58-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="56e58-225">Na liście aplikacji zaznacz **pliki M**.</span><span class="sxs-lookup"><span data-stu-id="56e58-225">In the applications list, select **M-Files**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="56e58-227">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="56e58-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="56e58-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="56e58-229">Click **Add** button.</span></span> <span data-ttu-id="56e58-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56e58-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="56e58-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="56e58-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="56e58-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56e58-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56e58-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56e58-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56e58-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="56e58-235">Testing single sign-on</span></span>

<span data-ttu-id="56e58-236">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="56e58-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="56e58-237">Po kliknięciu kafelka M pliki w panelu dostępu należy należy pobrać automatycznie zalogowane M pliki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56e58-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56e58-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="56e58-238">Additional resources</span></span>

* [<span data-ttu-id="56e58-239">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56e58-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56e58-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56e58-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

