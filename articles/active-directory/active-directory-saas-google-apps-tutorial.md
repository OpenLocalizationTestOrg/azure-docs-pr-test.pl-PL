---
title: "Samouczek: Integracji Azure Active Directory z usługi Google Apps w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="0b3aa-103">Samouczek: Integracji Azure Active Directory z usługi Google Apps</span><span class="sxs-lookup"><span data-stu-id="0b3aa-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="0b3aa-104">Z tego samouczka dowiesz się Integrowanie usługi Google Apps w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b3aa-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b3aa-105">Integrowanie usługi Google Apps z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b3aa-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługi Google Apps</span><span class="sxs-lookup"><span data-stu-id="0b3aa-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="0b3aa-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do aplikacji Google (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b3aa-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b3aa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0b3aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b3aa-109">Jeśli chcesz dowiedzieć się więcej informacji na temat integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b3aa-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b3aa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0b3aa-110">Prerequisites</span></span>

<span data-ttu-id="0b3aa-111">Aby skonfigurować integrację usługi Azure AD z usługi Google Apps, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="0b3aa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b3aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b3aa-113">Usługi Google Apps logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0b3aa-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b3aa-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b3aa-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b3aa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b3aa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b3aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="0b3aa-118">Samouczek wideo</span><span class="sxs-lookup"><span data-stu-id="0b3aa-118">Video tutorial</span></span>
<span data-ttu-id="0b3aa-119">Jak włączyć logowanie jednokrotne do aplikacji Google w ciągu 2 minut:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="0b3aa-120">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="0b3aa-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="0b3aa-121">**Pytanie: czy Chromebooks i innych urządzeniach Chrome zgodne z usługą Azure AD rejestracji jednokrotnej?**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="0b3aa-122">Odpowiedź: tak, użytkownicy będą mogli zalogować się do swoich urządzeń Chromebook przy użyciu swoich poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="0b3aa-123">Zobacz to [usługi Google Apps obsługuje artykułu](https://support.google.com/chrome/a/answer/6060880) informacji o tym, dlaczego użytkownicy mogą się monit o poświadczenia dwa razy.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="0b3aa-124">**Pytanie: czy włączyć logowanie jednokrotne, użytkownicy będą mogli używać swoich poświadczeń usługi Azure AD do logowania się do żadnego produktu Google, takich jak klasy Google, GMail, dysk Google, YouTube i tak dalej?**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="0b3aa-125">Odpowiedź: tak, w zależności od [aplikacje, które Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) chcesz włączyć lub wyłączyć w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="0b3aa-126">**Pytanie: czy można włączyć logowanie jednokrotne dla tylko podzestaw użytkowników usługi Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="0b3aa-127">A: wymaga włączenia logowania jednokrotnego natychmiast nie wszyscy użytkownicy usługi Google Apps do uwierzytelniania przy użyciu poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="0b3aa-128">Ponieważ usługi Google Apps nie obsługuje posiadanie wielu dostawców tożsamości, dostawca tożsamości w danym środowisku usługi Google Apps można usługi Azure AD lub Google —, ale nie oba jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="0b3aa-129">**Pytanie: czy użytkownik jest zalogowany przy użyciu systemu Windows, są one automatycznie uwierzytelniania do aplikacji Google bez pobierania zostanie wyświetlony monit o podanie hasła?**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="0b3aa-130">Odpowiedź: istnieją dwie opcje dotyczące włączania tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="0b3aa-131">Najpierw użytkownicy mogą zalogować się do urządzeń z systemem Windows 10 za pomocą [usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b3aa-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="0b3aa-132">Alternatywnie użytkownicy mogą zalogować się do urządzeń z systemem Windows, które są przyłączone do domeny do lokalnej usługi Active Directory, który został włączony dla pojedynczego logowania do usługi Azure AD za pomocą [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="0b3aa-133">Obie te opcje wymagają należy wykonać czynności opisane w następujących samouczkiem, aby włączyć logowanie jednokrotne między usługą Azure AD i usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b3aa-134">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0b3aa-134">Scenario description</span></span>
<span data-ttu-id="0b3aa-135">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b3aa-136">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b3aa-137">Dodawanie usługi Google Apps z galerii</span><span class="sxs-lookup"><span data-stu-id="0b3aa-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="0b3aa-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0b3aa-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="0b3aa-139">Dodawanie usługi Google Apps z galerii</span><span class="sxs-lookup"><span data-stu-id="0b3aa-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="0b3aa-140">Aby skonfigurować integrację usługi Google Apps w usłudze Azure Active Directory, należy dodać usługi Google Apps z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b3aa-141">**Aby dodać usługi Google Apps z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b3aa-142">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0b3aa-144">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b3aa-145">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-145">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0b3aa-147">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0b3aa-149">W polu wyszukiwania wpisz **usługi Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-149">In the search box, type **Google Apps**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="0b3aa-151">W panelu wyników wybierz **usługi Google Apps**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b3aa-153">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0b3aa-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b3aa-154">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="0b3aa-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b3aa-155">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, odpowiednik użytkownika usługi Google Apps jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="0b3aa-156">Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązane użytkownika usługi Google Apps musi określone.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="0b3aa-157">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="0b3aa-158">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b3aa-159">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b3aa-160">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b3aa-161">**[Tworzenie użytkownika testowego usługi Google Apps](#creating-a-google-apps-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta połączonego z usługi Azure AD reprezentację użytkownika usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b3aa-162">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b3aa-163">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b3aa-164">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0b3aa-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b3aa-165">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="0b3aa-166">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="0b3aa-167">W portalu Azure na **usługi Google Apps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0b3aa-169">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="0b3aa-171">Na **domenę usługi Google Apps i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="0b3aa-173">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="0b3aa-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b3aa-174">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-174">This value is not real.</span></span> <span data-ttu-id="0b3aa-175">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="0b3aa-176">Skontaktuj się z [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0b3aa-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="0b3aa-177">Na **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie Zapisz certyfikat na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="0b3aa-179">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-179">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b3aa-181">Na **Google Apps konfiguracji** kliknij **Konfigurowanie usługi Google Apps** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b3aa-182">Kopiuj **Sign-Out adres URL, SAML pojedynczy znak na adres URL usługi i zmień adres URL hasła** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="0b3aa-184">Otwórz nową kartę w przeglądarce i zaloguj się do [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="0b3aa-185">Kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-185">Click **Security**.</span></span> <span data-ttu-id="0b3aa-186">Jeśli nie widzisz łącza może być ukryty w obszarze **więcej formantów** menu u dołu ekranu.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Kliknij pozycję Zabezpieczenia.][10]

9. <span data-ttu-id="0b3aa-188">Na **zabezpieczeń** kliknij przycisk **Konfigurowanie rejestracji jednokrotnej (SSO).**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Kliknij przycisk logowania jednokrotnego.][11]

10. <span data-ttu-id="0b3aa-190">Wykonaj następujące zmiany w konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-190">Perform the following configuration changes:</span></span>
   
    ![Konfigurowanie logowania jednokrotnego][12]
   
    <span data-ttu-id="0b3aa-192">a.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-192">a.</span></span> <span data-ttu-id="0b3aa-193">Wybierz **Instalatora Usługa rejestracji Jednokrotnej z dostawcy tożsamości innych firm**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="0b3aa-194">b.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-194">b.</span></span> <span data-ttu-id="0b3aa-195">W **adres URL logowania strony** pola w usługi Google Apps, Wklej wartość **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0b3aa-196">c.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-196">c.</span></span> <span data-ttu-id="0b3aa-197">W **adres URL strony wylogowania** pola w usługi Google Apps, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0b3aa-198">d.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-198">d.</span></span> <span data-ttu-id="0b3aa-199">W **zmienić adres URL hasła** pola w usługi Google Apps, Wklej wartość **zmienić adres URL hasła**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0b3aa-200">e.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-200">e.</span></span> <span data-ttu-id="0b3aa-201">W usłudze Google Apps dla **certyfikatu weryfikacji**, Przekaż certyfikat, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="0b3aa-202">f.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-202">f.</span></span> <span data-ttu-id="0b3aa-203">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0b3aa-204">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="0b3aa-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b3aa-205">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b3aa-206">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b3aa-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b3aa-207">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b3aa-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b3aa-208">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0b3aa-210">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b3aa-211">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b3aa-213">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b3aa-215">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b3aa-217">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0b3aa-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b3aa-219">a.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-219">a.</span></span> <span data-ttu-id="0b3aa-220">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b3aa-221">b.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-221">b.</span></span> <span data-ttu-id="0b3aa-222">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b3aa-223">c.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-223">c.</span></span> <span data-ttu-id="0b3aa-224">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b3aa-225">d.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-225">d.</span></span> <span data-ttu-id="0b3aa-226">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="0b3aa-227">Tworzenie użytkownika testowego usługi Google Apps</span><span class="sxs-lookup"><span data-stu-id="0b3aa-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="0b3aa-228">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Google Apps oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="0b3aa-229">Usługi Google Apps obsługuje automatyczne Inicjowanie obsługi, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="0b3aa-230">Brak akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-230">There is no action for you in this section.</span></span> <span data-ttu-id="0b3aa-231">Jeśli użytkownik nie istnieje w oprogramowaniu do aplikacji Google, nowy jest tworzony podczas próby dostępu usługi Google Apps oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="0b3aa-232">Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0b3aa-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b3aa-233">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b3aa-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b3aa-234">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do aplikacji Google.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0b3aa-236">**Aby przypisać Simona Britta usługi Google Apps, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0b3aa-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="0b3aa-237">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0b3aa-239">Na liście aplikacji zaznacz **usługi Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-239">In the applications list, select **Google Apps**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="0b3aa-241">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0b3aa-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-243">Click **Add** button.</span></span> <span data-ttu-id="0b3aa-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0b3aa-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b3aa-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b3aa-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b3aa-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0b3aa-249">Testing single sign-on</span></span>

<span data-ttu-id="0b3aa-250">W tej sekcji, aby przetestować jednego ustawienia logowania jednokrotnego, otwórz panelu dostępu pod adresem [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), następnie zaloguj się do konta testowego i kliknij przycisk **usługi Google Apps** kafelka w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0b3aa-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b3aa-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0b3aa-251">Additional resources</span></span>

* [<span data-ttu-id="0b3aa-252">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b3aa-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b3aa-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b3aa-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0b3aa-254">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="0b3aa-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png