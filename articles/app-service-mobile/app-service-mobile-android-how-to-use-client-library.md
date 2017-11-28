---
title: aaaHow toouse hello Azure Mobile Apps SDK dla systemu Android | Dokumentacja firmy Microsoft
description: Jak toouse hello Azure Mobile Apps SDK dla systemu Android
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="d1773-103">Jak toouse hello Azure Mobile Apps SDK dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="d1773-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="d1773-104">Ten przewodnik przedstawia, jak toouse hello kliencką dla systemu Android SDK dla typowych scenariuszy tooimplement Mobile Apps, takich jak:</span><span class="sxs-lookup"><span data-stu-id="d1773-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="d1773-105">Wyszukiwanie danych (wstawiania, aktualizowania i usuwania).</span><span class="sxs-lookup"><span data-stu-id="d1773-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="d1773-106">Uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="d1773-106">Authentication.</span></span>
* <span data-ttu-id="d1773-107">Obsługa błędów.</span><span class="sxs-lookup"><span data-stu-id="d1773-107">Handling errors.</span></span>
* <span data-ttu-id="d1773-108">Dostosowywanie powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="d1773-108">Customizing hello client.</span></span>

<span data-ttu-id="d1773-109">Ten przewodnik koncentruje się na powitania klienta zestawu SDK systemu Android.</span><span class="sxs-lookup"><span data-stu-id="d1773-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="d1773-110">więcej informacji o toolearn hello zestawów SDK po stronie serwera dla Mobile Apps, zobacz [pracować z zaplecza .NET SDK] [ 10] lub [jak toouse hello zaplecza Node.js SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="d1773-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="d1773-111">Dokumentacji</span><span class="sxs-lookup"><span data-stu-id="d1773-111">Reference Documentation</span></span>

<span data-ttu-id="d1773-112">Można znaleźć hello [dokumentacja interfejsu API Javadocs] [ 12] hello biblioteki klienta dla systemu Android w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1773-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d1773-113">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="d1773-113">Supported Platforms</span></span>

<span data-ttu-id="d1773-114">Hello Azure Mobile Apps SDK dla systemu Android obsługuje poziom interfejsu API 19 do 24 (KitKat za pośrednictwem nugacie) Telefon i tablet rozmiarach.</span><span class="sxs-lookup"><span data-stu-id="d1773-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="d1773-115">Korzysta z uwierzytelniania, w szczególności wspólnej poświadczeń toogather podejście framework sieci web.</span><span class="sxs-lookup"><span data-stu-id="d1773-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="d1773-116">Uwierzytelnianie serwera przepływu nie działa z niewielkich współczynnik urządzeń, takich jak obserwowanie.</span><span class="sxs-lookup"><span data-stu-id="d1773-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="d1773-117">Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1773-117">Setup and Prerequisites</span></span>

<span data-ttu-id="d1773-118">Zakończenie hello [szybkiego startu Mobile Apps](app-service-mobile-android-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="d1773-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="d1773-119">To zadanie gwarantuje, że zostały spełnione wszystkie wymagania wstępne związane z opracowywaniem Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="d1773-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="d1773-120">Witaj szybkiego startu pomaga również skonfigurować konta i utworzyć pierwszy zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="d1773-121">Jeśli zdecydujesz się nie toocomplete samouczek Szybki Start — Witaj, wykonaj hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d1773-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="d1773-122">[Tworzenie zaplecza aplikacji mobilnej] [ 13] toouse z aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="d1773-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="d1773-123">W programie Android Studio [hello aktualizacji Gradle kompilacja plików](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="d1773-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="d1773-124">[Włącz uprawnień internetowych](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="d1773-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="d1773-125"><a name="gradle-build"></a>Aktualizacja hello Gradle kompilacji pliku</span><span class="sxs-lookup"><span data-stu-id="d1773-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="d1773-126">Zmiana obu **build.gradle** plików:</span><span class="sxs-lookup"><span data-stu-id="d1773-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="d1773-127">Dodaj ten kod toohello *projektu* poziom **build.gradle** pliku wewnątrz hello *buildscript* tagu:</span><span class="sxs-lookup"><span data-stu-id="d1773-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="d1773-128">Dodaj ten kod toohello *aplikacji modułu* poziom **build.gradle** pliku wewnątrz hello *zależności* tagu:</span><span class="sxs-lookup"><span data-stu-id="d1773-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="d1773-129">Najnowsza wersja hello jest obecnie 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="d1773-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="d1773-130">Witaj obsługiwane wersje są wymienione [w serwisie bintray][14].</span><span class="sxs-lookup"><span data-stu-id="d1773-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="d1773-131"><a name="enable-internet"></a>Włącz uprawnień internetowych</span><span class="sxs-lookup"><span data-stu-id="d1773-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="d1773-132">tooaccess Azure aplikacji musi mieć włączone uprawnienia INTERNET hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="d1773-133">Jeśli nie zostało jeszcze jest włączone, należy dodać powitania po wierszu kodu tooyour **AndroidManifest.xml** pliku:</span><span class="sxs-lookup"><span data-stu-id="d1773-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="d1773-134">Utwórz połączenie klienta</span><span class="sxs-lookup"><span data-stu-id="d1773-134">Create a Client Connection</span></span>

<span data-ttu-id="d1773-135">Azure Mobile Apps udostępnia cztery funkcje tooyour aplikacji mobilnej:</span><span class="sxs-lookup"><span data-stu-id="d1773-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="d1773-136">Dostęp do danych i synchronizacji z usługą Azure Mobile Services aplikacje w trybie Offline.</span><span class="sxs-lookup"><span data-stu-id="d1773-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="d1773-137">Wywoływania niestandardowych interfejsów API napisany za pomocą hello zestaw SDK usługi Azure Mobile Apps serwera.</span><span class="sxs-lookup"><span data-stu-id="d1773-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="d1773-138">Uwierzytelnianie za pomocą usługi aplikacji Azure uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="d1773-139">Rejestracja powiadomień z koncentratorami powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="d1773-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="d1773-140">Każda z tych funkcji wymaga najpierw utworzenia `MobileServiceClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d1773-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="d1773-141">Tylko jeden `MobileServiceClient` obiekt powinien zostać utworzony w ramach sieci klientów urządzeń przenośnych (to znaczy, należy go wzorzec Singleton).</span><span class="sxs-lookup"><span data-stu-id="d1773-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="d1773-142">toocreate `MobileServiceClient` obiektu:</span><span class="sxs-lookup"><span data-stu-id="d1773-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="d1773-143">Witaj `<MobileAppUrl>` to ciąg lub obiekt adres URL, który wskazuje tooyour zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="d1773-144">Jeśli używasz usługi Azure App Service toohost z zaplecza aplikacji mobilnych, upewnij się, użyj hello bezpiecznego `https://` wersji hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d1773-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="d1773-145">powitania klienta wymaga również toohello dostępu działania lub kontekstu — Witaj `this` parametru w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="d1773-146">Hello konstrukcji MobileServiceClient powinno się zdarzyć w hello `onCreate()` metody hello w hello odwoływać się działanie `AndroidManifest.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="d1773-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="d1773-147">Jako najlepsze rozwiązanie należy abstrakcyjnej komunikacji z serwerem do własnej klasy (wzorca singleton).</span><span class="sxs-lookup"><span data-stu-id="d1773-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="d1773-148">W takim przypadku należy przekazać hello działania w ramach tooappropriately Konstruktor hello skonfigurować usługę hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="d1773-149">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d1773-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="d1773-150">Można teraz wywołać `AzureServiceAdapter.Initialize(this);` w hello `onCreate()` metody działania głównego.</span><span class="sxs-lookup"><span data-stu-id="d1773-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="d1773-151">Użyj innych metod wymagające dostępu klienta toohello `AzureServiceAdapter.getInstance();` tooobtain karty usługi toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="d1773-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="d1773-152">Operacje na danych</span><span class="sxs-lookup"><span data-stu-id="d1773-152">Data Operations</span></span>

<span data-ttu-id="d1773-153">Hello najważniejsza część hello Azure Mobile Apps SDK jest toodata dostępu tooprovide przechowywane w ramach usług SQL Azure na powitania zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="d1773-154">Można uzyskać dostępu do te dane przy użyciu klasy jednoznacznie (preferowane) lub wykonywania kwerend (niezalecane).</span><span class="sxs-lookup"><span data-stu-id="d1773-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="d1773-155">zbiorcze Hello przedstawione w tej sekcji zajmuje się przy użyciu silnie typizowanej klasy.</span><span class="sxs-lookup"><span data-stu-id="d1773-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="d1773-156">Definiowanie klas danych klienta</span><span class="sxs-lookup"><span data-stu-id="d1773-156">Define client data classes</span></span>

<span data-ttu-id="d1773-157">tooaccess dane z tabel SQL Azure, definiowania klas danych klienta, które odpowiadają toohello tabel w hello zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="d1773-158">Przykłady w tym temacie założono tabela o nazwie **MyDataTable**, która zawiera następujące kolumny hello:</span><span class="sxs-lookup"><span data-stu-id="d1773-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="d1773-159">id</span><span class="sxs-lookup"><span data-stu-id="d1773-159">id</span></span>
* <span data-ttu-id="d1773-160">Tekst</span><span class="sxs-lookup"><span data-stu-id="d1773-160">text</span></span>
* <span data-ttu-id="d1773-161">Zakończenie</span><span class="sxs-lookup"><span data-stu-id="d1773-161">complete</span></span>

<span data-ttu-id="d1773-162">Witaj odpowiedni obiekt typu po stronie klienta znajduje się w pliku o nazwie **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="d1773-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="d1773-163">Dodaj metody pobierającej i ustawiającej dla każdego pola, które można dodać.</span><span class="sxs-lookup"><span data-stu-id="d1773-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="d1773-164">Jeśli tabela SQL Azure zawiera więcej kolumn, należy dodać hello odpowiadającą klasę toothis pola.</span><span class="sxs-lookup"><span data-stu-id="d1773-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="d1773-165">Na przykład, jeśli hello DTO kolumna priorytet liczb całkowitych miał (obiektu transferu danych), a następnie można dodać tego pola, wraz z jego metody pobierającej i ustawiającej:</span><span class="sxs-lookup"><span data-stu-id="d1773-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="d1773-166">toolearn toocreate dodatkowe tabele w zapleczu swojej Mobile Apps, zobacz temat [porady: Definiowanie kontrolera tabeli] [ 15] (zaplecze .NET) lub [zdefiniuj tabel za pomocą dynamicznej schematu] [ 16] (Zaplecza Node.js).</span><span class="sxs-lookup"><span data-stu-id="d1773-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="d1773-167">Azure Mobile Apps tabeli wewnętrznej bazy danych definiuje pięć specjalne pól, z których cztery są dostępne tooclients:</span><span class="sxs-lookup"><span data-stu-id="d1773-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="d1773-168">`String id`: hello globalnie unikatowy identyfikator hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="d1773-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="d1773-169">Jako najlepsze rozwiązanie należy hello identyfikator hello reprezentację ciągu [UUID] [ 17] obiektu.</span><span class="sxs-lookup"><span data-stu-id="d1773-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="d1773-170">`DateTimeOffset updatedAt`: hello Data/godzina ostatniej aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="d1773-171">Witaj updatedAt pola jest ustawiana przez powitania serwera i nie powinno być używane przez kod klienta.</span><span class="sxs-lookup"><span data-stu-id="d1773-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="d1773-172">`DateTimeOffset createdAt`: hello daty i godziny utworzenia tego obiektu hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="d1773-173">Witaj createdAt pola jest ustawiana przez powitania serwera i nie powinno być używane przez kod klienta.</span><span class="sxs-lookup"><span data-stu-id="d1773-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="d1773-174">`byte[] version`: Zazwyczaj reprezentowany jako ciąg, wersja hello jest również ustawić powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="d1773-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="d1773-175">`boolean deleted`: Wskazuje, że rekord hello została usunięta, ale nie są przeczyszczane jeszcze.</span><span class="sxs-lookup"><span data-stu-id="d1773-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="d1773-176">Nie używaj `deleted` jako właściwość w klasie.</span><span class="sxs-lookup"><span data-stu-id="d1773-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="d1773-177">Witaj `id` pole jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="d1773-177">hello `id` field is required.</span></span>  <span data-ttu-id="d1773-178">Witaj `updatedAt` pola i `version` pola są używane do synchronizacji w trybie offline (przyrostowej synchronizacji i wystąpi konflikt rozpoznawania odpowiednio).</span><span class="sxs-lookup"><span data-stu-id="d1773-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="d1773-179">Witaj `createdAt` pole jest polem Odwołanie i nie jest używana przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="d1773-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="d1773-180">nazwy Hello "w locie" nazwy właściwości hello i nie są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="d1773-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="d1773-181">Jednak można utworzyć mapowania między obiektu i hello "w locie" nazw przy użyciu hello [gson] [ 3] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d1773-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="d1773-182">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d1773-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="d1773-183">Tworzenie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="d1773-183">Create a Table Reference</span></span>

<span data-ttu-id="d1773-184">tooaccess tabeli, najpierw utwórz [MobileServiceTable] [ 8] obiektu wywołującego hello **getTable** metody na powitania [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="d1773-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="d1773-185">Ta metoda ma dwa przeciążenia:</span><span class="sxs-lookup"><span data-stu-id="d1773-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="d1773-186">W hello następującego kodu **mClient** jest obiektem MobileServiceClient tooyour odwołania.</span><span class="sxs-lookup"><span data-stu-id="d1773-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="d1773-187">przeciążenia pierwszy Hello jest używany, gdzie hello nazwę klasy i nazwę tabeli hello są hello takie same i hello jeden służy w hello Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="d1773-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="d1773-188">Witaj przeciążenia drugi jest używany podczas hello Nazwa tabeli jest inna niż nazwa klasy hello: hello pierwszym parametrem jest hello nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="d1773-189"><a name="query"></a>Zapytania dotyczącego tabeli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d1773-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="d1773-190">Najpierw należy uzyskać odwołania do tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-190">First, obtain a table reference.</span></span>  <span data-ttu-id="d1773-191">Następnie można wykonać zapytania na powitania odwołanie do tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="d1773-192">Zapytanie jest dowolną kombinację:</span><span class="sxs-lookup"><span data-stu-id="d1773-192">A query is any combination of:</span></span>

* <span data-ttu-id="d1773-193">A `.where()` [klauzuli filtru](#filtering).</span><span class="sxs-lookup"><span data-stu-id="d1773-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="d1773-194">`.orderBy()` [Porządkowanie klauzuli](#sorting).</span><span class="sxs-lookup"><span data-stu-id="d1773-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="d1773-195">A `.select()` [pola wyboru klauzuli](#selection).</span><span class="sxs-lookup"><span data-stu-id="d1773-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="d1773-196">A `.skip()` i `.top()` dla [stronicowanej wyniki](#paging).</span><span class="sxs-lookup"><span data-stu-id="d1773-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="d1773-197">klauzule Hello przedstawia w hello poprzedzających kolejności.</span><span class="sxs-lookup"><span data-stu-id="d1773-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="d1773-198"><a name="filter"></a>Filtrowanie wyników</span><span class="sxs-lookup"><span data-stu-id="d1773-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="d1773-199">Formularz ogólny Hello zapytania jest:</span><span class="sxs-lookup"><span data-stu-id="d1773-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="d1773-200">Witaj poprzedni przykład zwraca wszystkie wyniki (up toohello maksymalny rozmiar strony ustawione przez powitania serwera).</span><span class="sxs-lookup"><span data-stu-id="d1773-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="d1773-201">Witaj `.execute()` metoda wykonuje zapytanie hello hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="d1773-202">Hello zapytanie jest przekonwertowanego tooan [OData v3] [ 19] zapytania przed transmisji toohello Mobile Apps wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="d1773-203">Po otrzymaniu zaplecza aplikacji mobilnej hello konwertuje hello zapytania do instrukcji SQL przed jej wykonanie w wystąpieniu SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="d1773-204">Ponieważ działania sieci dopiero po pewnym czasie, hello `.execute()` metoda zwraca [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="d1773-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="d1773-205"><a name="filtering"></a>Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="d1773-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="d1773-206">powitania po wykonywania zapytania zwraca wszystkie elementy z hello **ToDoItem** tabeli where **pełną** jest równe **false**.</span><span class="sxs-lookup"><span data-stu-id="d1773-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="d1773-207">**mToDoTable** jest hello odwołanie toohello usługi mobilnej tabeli utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d1773-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="d1773-208">Zdefiniuj filtr przy użyciu hello **gdzie** wywołanie metody hello w odwołaniu do tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="d1773-209">Witaj **gdzie** następuje — metoda **pola** metody następuje metodę, która określa hello logicznej predykatu.</span><span class="sxs-lookup"><span data-stu-id="d1773-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="d1773-210">Predykatu metod uwzględnić **eq** (równe), **ne** (nie równa), **gt** (większe niż) **ge** (większe lub równe), **lt** (poniżej), **le** (mniejsze niż lub równe).</span><span class="sxs-lookup"><span data-stu-id="d1773-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="d1773-211">Te metody umożliwiają porównanie liczby i toospecific wartości w polach ciąg.</span><span class="sxs-lookup"><span data-stu-id="d1773-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="d1773-212">Można filtrować według daty.</span><span class="sxs-lookup"><span data-stu-id="d1773-212">You can filter on dates.</span></span> <span data-ttu-id="d1773-213">Hello następujące metody umożliwiają porównanie hello Data całego lub części daty hello: **roku**, **miesiąca**, **dzień**, **godzinę**, **minutę**, i **drugi**.</span><span class="sxs-lookup"><span data-stu-id="d1773-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="d1773-214">Witaj poniższy przykład umożliwia dodanie filtru dla elementów których *termin* jest równe 2013.</span><span class="sxs-lookup"><span data-stu-id="d1773-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="d1773-215">Witaj następujących metod obsługi złożonych filtrów na pól ciągów: **startsWith**, **endsWith**, **concat**, **podciąg**, **indexOf**, **Zastąp**, **toLower**, **toUpper**, **trim**, i  **długość**.</span><span class="sxs-lookup"><span data-stu-id="d1773-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="d1773-216">następujące przykładowe filtry dla tabeli wiersze, w których hello Hello *tekst* kolumny rozpoczyna się od "PRI0."</span><span class="sxs-lookup"><span data-stu-id="d1773-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="d1773-217">następujące metody operator Hello są obsługiwane w pola liczb: **dodać**, **sub**, **mul**, **div**, **mod**, **floor**, **limitu**, i **zaokrąglona**.</span><span class="sxs-lookup"><span data-stu-id="d1773-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="d1773-218">następujące przykładowe filtry dla tabeli wiersze, w których hello Hello **czas trwania** jest liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="d1773-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="d1773-219">Predykaty można połączyć z tych metod logiczne: **i**, **lub** i **nie**.</span><span class="sxs-lookup"><span data-stu-id="d1773-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="d1773-220">Poniższy przykład Hello łączy dwa hello poprzedzających przykłady.</span><span class="sxs-lookup"><span data-stu-id="d1773-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="d1773-221">Operatory logiczne grupy i gniazda:</span><span class="sxs-lookup"><span data-stu-id="d1773-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="d1773-222">Aby uzyskać bardziej szczegółowe omówienie i przykłady filtrowania, zobacz [eksploracji siłę hello powitania klienta dla systemu Android zapytania modelu][20].</span><span class="sxs-lookup"><span data-stu-id="d1773-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="d1773-223"><a name="sorting"></a>Sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="d1773-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="d1773-224">Witaj następujący kod zwraca wszystkie elementy z tabeli z **ToDoItems** sortowane rosnąco przez hello *tekst* pola.</span><span class="sxs-lookup"><span data-stu-id="d1773-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="d1773-225">*mToDoTable* jest hello toohello zaplecza spis utworzonego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d1773-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="d1773-226">pierwszy parametr hello Hello **orderBy** — metoda jest nazwą równy toohello ciąg hello pola, w których toosort.</span><span class="sxs-lookup"><span data-stu-id="d1773-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="d1773-227">drugi parametr Hello używa hello **QueryOrder** toospecify wyliczenie czy toosort w kolejności rosnącej lub malejącej.</span><span class="sxs-lookup"><span data-stu-id="d1773-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="d1773-228">Jeśli są filtrowanie przy użyciu hello ***gdzie*** metoda, hello ***gdzie*** metody należy wywołać przed hello ***orderBy*** — metoda.</span><span class="sxs-lookup"><span data-stu-id="d1773-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="d1773-229"><a name="selection"></a>Wybrać określone kolumny</span><span class="sxs-lookup"><span data-stu-id="d1773-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="d1773-230">Hello poniższy kod ilustruje sposób tooreturn wszystkich elementów z tabeli **ToDoItems**, ale wyświetlane są tylko hello **pełną** i **tekst** pola.</span><span class="sxs-lookup"><span data-stu-id="d1773-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="d1773-231">**mToDoTable** jest hello odwołanie toohello zaplecza tabeli utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d1773-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="d1773-232">Funkcja wybierz toohello parametry Hello są nazwami ciąg hello hello tabeli kolumn, które mają tooreturn.</span><span class="sxs-lookup"><span data-stu-id="d1773-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="d1773-233">Witaj **wybierz** metody musi toofollow metody, takie jak **gdzie** i **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="d1773-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="d1773-234">Może występować przez metody stronicowania, takie jak **pominąć** i **górnej**.</span><span class="sxs-lookup"><span data-stu-id="d1773-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="d1773-235"><a name="paging"></a>Zwróć dane strony</span><span class="sxs-lookup"><span data-stu-id="d1773-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="d1773-236">Dane są **zawsze** zwracane w stronach.</span><span class="sxs-lookup"><span data-stu-id="d1773-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="d1773-237">Witaj maksymalną liczbę rekordów zwróconych jest ustawiana przez serwer hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="d1773-238">Jeśli powitania klienta żąda więcej rekordów, powitania serwera zwraca hello maksymalną liczbę rekordów.</span><span class="sxs-lookup"><span data-stu-id="d1773-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="d1773-239">Domyślnie program hello maksymalny rozmiar strony na powitania serwera jest 50 rekordów.</span><span class="sxs-lookup"><span data-stu-id="d1773-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="d1773-240">Hello pierwszym przykładzie pokazano, jak tooselect hello pierwsze pięć elementy z tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="d1773-241">Hello zapytanie zwraca hello elementów z tabeli z **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="d1773-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="d1773-242">**mToDoTable** jest hello toohello zaplecza spis utworzonego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d1773-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="d1773-243">Oto zapytania, że pomija hello pięć pierwszych elementów, a następnie zwraca hello następnych pięciu:</span><span class="sxs-lookup"><span data-stu-id="d1773-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="d1773-244">Jeśli chcesz tooget wszystkie rekordy w tabeli, należy zaimplementować tooiterate kodu za pośrednictwem wszystkich stron:</span><span class="sxs-lookup"><span data-stu-id="d1773-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="d1773-245">Żądanie dla wszystkich rekordów za pomocą tej metody tworzy co najmniej dwa żądania toohello Mobile Apps wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="d1773-246">Wybieranie rozmiaru prawej strony hello jest kompromis między użycia pamięci podczas żądania hello jest wykonywane, przepustowości i opóźnień w całkowicie odbieranie danych hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="d1773-247">domyślne Hello (50 rekordów) jest odpowiednia dla wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d1773-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="d1773-248">Wyłącznie w przypadku obsługi większych urządzeń pamięci, należy zwiększyć się too500.</span><span class="sxs-lookup"><span data-stu-id="d1773-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="d1773-249">Znaleziono ten zwiększa rozmiar strony hello ponad 500 rejestruje wyniki nie do przyjęcia opóźnienia i problemy z dużej ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="d1773-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="d1773-250"><a name="chaining"></a>Porady: łączenie metody zapytania</span><span class="sxs-lookup"><span data-stu-id="d1773-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="d1773-251">może zostać dołączona metody Hello badania tabel wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="d1773-252">Tworzenie łańcuchów metody umożliwia tooselect określonych kolumn filtrowane wierszy, które są sortowane i stronicowane zapytanie.</span><span class="sxs-lookup"><span data-stu-id="d1773-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="d1773-253">Można tworzyć złożone filtry logiczne.</span><span class="sxs-lookup"><span data-stu-id="d1773-253">You can create complex logical filters.</span></span>  <span data-ttu-id="d1773-254">Każda metoda zapytanie zwraca obiekt zapytania.</span><span class="sxs-lookup"><span data-stu-id="d1773-254">Each query method returns a Query object.</span></span> <span data-ttu-id="d1773-255">ciąg hello tooend metod i hello faktycznie wykonywania zapytania, wywołanie hello **wykonania** metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="d1773-256">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d1773-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="d1773-257">Witaj powiązane zapytania metody muszą być uporządkowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d1773-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="d1773-258">Filtrowanie (**gdzie**) metod.</span><span class="sxs-lookup"><span data-stu-id="d1773-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="d1773-259">Sortowanie (**orderBy**) metod.</span><span class="sxs-lookup"><span data-stu-id="d1773-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="d1773-260">Wybór (**wybierz**) metod.</span><span class="sxs-lookup"><span data-stu-id="d1773-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="d1773-261">stronicowanie (**pominąć** i **górnej**) metod.</span><span class="sxs-lookup"><span data-stu-id="d1773-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="d1773-262"><a name="binding"></a>Powiąż interfejsu użytkownika toohello danych</span><span class="sxs-lookup"><span data-stu-id="d1773-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="d1773-263">Powiązanie danych obejmuje trzy składniki:</span><span class="sxs-lookup"><span data-stu-id="d1773-263">Data binding involves three components:</span></span>

* <span data-ttu-id="d1773-264">Witaj źródła danych</span><span class="sxs-lookup"><span data-stu-id="d1773-264">hello data source</span></span>
* <span data-ttu-id="d1773-265">Witaj układu ekranu</span><span class="sxs-lookup"><span data-stu-id="d1773-265">hello screen layout</span></span>
* <span data-ttu-id="d1773-266">Karta Hello czy ties Witaj dwie razem.</span><span class="sxs-lookup"><span data-stu-id="d1773-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="d1773-267">W naszym przykładowym kodzie hello danych zwróconych z tabeli Mobile Apps SQL Azure hello **ToDoItem** do tablicy.</span><span class="sxs-lookup"><span data-stu-id="d1773-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="d1773-268">To działanie jest wspólnego wzorca dla danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="d1773-269">Zapytania bazy danych często zwracać kolekcji wierszy, które hello klient pobiera listy lub tablicy.</span><span class="sxs-lookup"><span data-stu-id="d1773-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="d1773-270">W tym przykładzie tablica hello jest hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="d1773-271">Kod Hello określa układ ekranu, definiujący widok hello hello dane wyświetlane na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="d1773-272">Witaj dwie powiązanych wraz z karty, którego ten kod jest rozszerzeniem hello **ArrayAdapter&lt;ToDoItem&gt;**  klasy.</span><span class="sxs-lookup"><span data-stu-id="d1773-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="d1773-273"><a name="layout"></a>Zdefiniuj hello układu</span><span class="sxs-lookup"><span data-stu-id="d1773-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="d1773-274">Witaj układ jest definiowany przez kilka fragmentów kodu XML.</span><span class="sxs-lookup"><span data-stu-id="d1773-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="d1773-275">Biorąc pod uwagę istniejącego układu, hello następującego kodu reprezentuje hello **ListView** chcemy toopopulate z naszych danych serwera.</span><span class="sxs-lookup"><span data-stu-id="d1773-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="d1773-276">W hello poprzedzających kodu, hello *listitem* atrybut określa identyfikator hello hello układu dla pojedynczego wiersza na liście hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="d1773-277">Ten kod pobiera utworzyć raz dla każdego elementu na liście hello i określa pole wyboru i jego tekst.</span><span class="sxs-lookup"><span data-stu-id="d1773-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="d1773-278">Ten układ nie wyświetla hello **identyfikator** pola i bardziej złożonej układu określić dodatkowe pola hello wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="d1773-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="d1773-279">Ten kod jest hello **row_list_to_do.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="d1773-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="d1773-280"><a name="adapter"></a>Zdefiniuj hello karty</span><span class="sxs-lookup"><span data-stu-id="d1773-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="d1773-281">Ponieważ źródło danych hello naszych widoku jest tablicą **ToDoItem**, możemy podklasy naszych karty z **ArrayAdapter&lt;ToDoItem&gt;**  klasy.</span><span class="sxs-lookup"><span data-stu-id="d1773-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="d1773-282">To podklasa tworzy widok dla każdego **ToDoItem** przy użyciu hello **row_list_to_do** układu.</span><span class="sxs-lookup"><span data-stu-id="d1773-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="d1773-283">W naszym kodzie zdefiniować następujące klasy, która jest rozszerzeniem hello hello **ArrayAdapter&lt;E&gt;**  klasy:</span><span class="sxs-lookup"><span data-stu-id="d1773-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="d1773-284">Zastąpienie kart hello **getView** metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="d1773-285">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d1773-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="d1773-286">Tworzymy wystąpienie tej klasy w naszych działań w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d1773-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="d1773-287">Witaj drugi parametr toohello ToDoItemAdapter Konstruktor jest układ toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="d1773-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="d1773-288">Firma Microsoft może teraz utworzyć wystąpienia hello **ListView** i przypisz hello karty toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="d1773-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="d1773-289"><a name="use-adapter"></a>Użyj hello karty tooBind toohello interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d1773-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="d1773-290">Wszystko jest teraz gotowy toouse powiązania danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="d1773-291">Witaj poniższy kod przedstawia sposób tooget elementów w tabeli hello i wypełnienia hello karty lokalnej z hello zwracane elementy.</span><span class="sxs-lookup"><span data-stu-id="d1773-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="d1773-292">Wywołaj karty hello kiedykolwiek zmodyfikujesz hello **ToDoItem** tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="d1773-293">Ponieważ zmiany są wykonywane na podstawie rekordu na podstawie, można obsługiwać pojedynczy wiersz zamiast kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1773-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="d1773-294">Po wstawieniu elementu wywołać hello **dodać** — metoda na hello karty; podczas usuwania, wywołaj hello **Usuń** — metoda.</span><span class="sxs-lookup"><span data-stu-id="d1773-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="d1773-295">Pełny przykład można znaleźć w hello [projektu szybkiego startu dla systemu Android][21].</span><span class="sxs-lookup"><span data-stu-id="d1773-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="d1773-296"><a name="inserting"></a>Wstawianie danych do hello wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d1773-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="d1773-297">Tworzy wystąpienie hello *ToDoItem* klasy i ustawienia swoich właściwości.</span><span class="sxs-lookup"><span data-stu-id="d1773-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="d1773-298">Następnie użyj **operacji insert()** tooinsert obiektu:</span><span class="sxs-lookup"><span data-stu-id="d1773-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="d1773-299">Hello zwrócił zgodne jednostki danych hello wstawione do tabeli wewnętrznej bazy danych hello, identyfikator hello dołączone i inne wartości (takie jak hello `createdAt`, `updatedAt`, i `version` pól) Ustaw hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="d1773-300">Tabele Mobile Apps, wymagają kolumna klucza podstawowego o nazwie **identyfikator**. Ta kolumna musi być ciągiem.</span><span class="sxs-lookup"><span data-stu-id="d1773-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="d1773-301">Wartość domyślna Hello hello identyfikator kolumny jest identyfikatorem GUID.</span><span class="sxs-lookup"><span data-stu-id="d1773-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="d1773-302">Możesz podać inne unikatowe wartości, takie jak adresy e-mail lub nazwy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d1773-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="d1773-303">Nie podano wartość Identyfikatora ciągu wstawionego rekordu, zaplecza hello generuje nowy identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="d1773-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="d1773-304">Ciąg Identyfikatora wartości zawierają hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d1773-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="d1773-305">Identyfikatory mogą być generowane bez wprowadzania toohello obiegu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="d1773-306">Rekordy są łatwiejsze toomerge z różnych tabel lub baz danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="d1773-307">Wartości Identyfikatora lepszą integrację z logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="d1773-308">Ciąg Identyfikatora wartości są **REQUIRED** obsługę synchronizacji w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="d1773-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="d1773-309">Nie można zmienić identyfikatora, gdy jest on przechowywany w hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="d1773-310"><a name="updating"></a>Aktualizuj dane w aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="d1773-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="d1773-311">tooupdate dane w tabeli, Przekaż hello nowy obiekt toohello **update()** metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="d1773-312">W tym przykładzie *elementu* jest odwołanie do wiersza tooa hello *ToDoItem* tabeli, które były tooit niektóre zmiany wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="d1773-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="d1773-313">Hello wiersz z hello sam **identyfikator** jest aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="d1773-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="d1773-314"><a name="deleting"></a>Usuwanie danych w aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="d1773-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="d1773-315">Witaj następującego kodu pokazuje, jak toodelete danych z tabeli, określając hello obiektu danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="d1773-316">Można również usunąć element, określając hello **identyfikator** pole hello toodelete wiersza.</span><span class="sxs-lookup"><span data-stu-id="d1773-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="d1773-317"><a name="lookup"></a>Wyszukiwanie określonego elementu według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="d1773-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="d1773-318">Wyszukiwanie elementu z określonym **identyfikator** pole z hello **lookUp()** metody:</span><span class="sxs-lookup"><span data-stu-id="d1773-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="d1773-319"><a name="untyped"></a>Porady: Praca z danymi bez typu</span><span class="sxs-lookup"><span data-stu-id="d1773-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="d1773-320">model programowania bez typu Hello zapewnia dokładną kontrolę nad serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="d1773-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="d1773-321">Brak niektórych typowych scenariuszy, w którym możesz toouse model programowania bez typu.</span><span class="sxs-lookup"><span data-stu-id="d1773-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="d1773-322">Na przykład, jeśli tabela wewnętrznej bazy danych zawiera wiele kolumn, wystarczy tooreference podzbiór hello kolumn.</span><span class="sxs-lookup"><span data-stu-id="d1773-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="d1773-323">model typu Hello wymaga toodefine wszystkich kolumn hello zdefiniowanych w hello zaplecza aplikacji mobilnej w klasie danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="d1773-324">Większość hello wywołania interfejsu API w celu uzyskania dostępu do danych są podobne toohello wpisane wywołania programowania.</span><span class="sxs-lookup"><span data-stu-id="d1773-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="d1773-325">Witaj podstawowa różnica polega na czy w modelu bez typu hello można wywołać metod w hello **MobileServiceJsonTable** obiektu zamiast hello **MobileServiceTable** obiektu.</span><span class="sxs-lookup"><span data-stu-id="d1773-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="d1773-326"><a name="json_instance"></a>Utwórz wystąpienie tabeli bez typu</span><span class="sxs-lookup"><span data-stu-id="d1773-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="d1773-327">Podobne toohello wpisane modelu, możesz uruchomić pobierania odwołania do tabeli, ale w tym przypadku jest **MobileServicesJsonTable** obiektu.</span><span class="sxs-lookup"><span data-stu-id="d1773-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="d1773-328">Uzyskaj odwołanie hello przez wywołanie hello **getTable** metody w wystąpieniu powitania klienta:</span><span class="sxs-lookup"><span data-stu-id="d1773-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="d1773-329">Po utworzeniu wystąpienia hello **MobileServiceJsonTable**, praktycznie ma tekst hello tego samego interfejsu API, które są dostępne jako z modelem programowania typu hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="d1773-330">W niektórych przypadkach hello metody przyjmują bez typu parametru zamiast parametru typu.</span><span class="sxs-lookup"><span data-stu-id="d1773-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="d1773-331"><a name="json_insert"></a>Wstaw do tabeli bez typu</span><span class="sxs-lookup"><span data-stu-id="d1773-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="d1773-332">Witaj następującego kodu pokazuje sposób toodo insert.</span><span class="sxs-lookup"><span data-stu-id="d1773-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="d1773-333">Witaj pierwszym krokiem jest toocreate [JsonObject][1], który jest częścią hello [gson] [ 3] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d1773-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="d1773-334">Następnie należy użyć **operacji insert()** tooinsert hello nieuwzględniające typów obiektów do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="d1773-335">Jeśli potrzebny jest identyfikator hello tooget hello wstawić obiektu, użyj hello **getAsJsonPrimitive()** metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="d1773-336"><a name="json_delete"></a>Usuń z tabeli bez typu</span><span class="sxs-lookup"><span data-stu-id="d1773-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="d1773-337">Witaj poniższy kod przedstawia sposób toodelete instancję, w tym przypadku hello tego samego wystąpienia **JsonObject** utworzony we wcześniejszej hello *Wstaw* przykład.</span><span class="sxs-lookup"><span data-stu-id="d1773-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="d1773-338">Kod Hello jest hello takie same jak w przypadku hello wpisane przypadek, ale metoda hello ma inny podpis, ponieważ odwołuje się on **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="d1773-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="d1773-339">Możesz także usunąć wystąpienia bezpośrednio za pomocą jego Identyfikatora:</span><span class="sxs-lookup"><span data-stu-id="d1773-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="d1773-340"><a name="json_get"></a>Zwracanie wszystkich wierszy z tabeli bez typu</span><span class="sxs-lookup"><span data-stu-id="d1773-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="d1773-341">Witaj następującego kodu pokazuje sposób tooretrieve całej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1773-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="d1773-342">Ponieważ używasz tabeli JSON, można selektywnie pobierać tylko niektóre kolumny tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="d1773-343">Witaj tego samego zestawu filtrowania, filtrowania i stronicowania metod, które są dostępne dla modelu typu hello są dostępne dla hello bez typu modelu.</span><span class="sxs-lookup"><span data-stu-id="d1773-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="d1773-344"><a name="offline-sync"></a>Implementowanie synchronizacji w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="d1773-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="d1773-345">Witaj zestawu SDK klienta usługi Azure Mobile Apps implementuje również synchronizacji danych w trybie offline przy użyciu kopii danych serwera hello toostore bazy danych SQLite lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d1773-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="d1773-346">Operacje wykonywane w trybie offline tabeli nie wymagają toowork łączność.</span><span class="sxs-lookup"><span data-stu-id="d1773-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="d1773-347">Synchronizacja w trybie offline pomaga odporności i wydajności na powitania koszt bardziej złożonej logiki do rozwiązywania konfliktów.</span><span class="sxs-lookup"><span data-stu-id="d1773-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="d1773-348">Witaj zestawu SDK klienta usługi Azure Mobile Apps implementuje hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="d1773-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="d1773-349">Synchronizacja przyrostowa: Tylko zaktualizowanych i nowych rekordów są pobierane, zapisywanie zużycie przepustowości i pamięci.</span><span class="sxs-lookup"><span data-stu-id="d1773-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="d1773-350">Optymistycznej współbieżności: Operacje są uznawane za toosucceed.</span><span class="sxs-lookup"><span data-stu-id="d1773-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="d1773-351">Rozwiązywanie konfliktów jest odłożona do aktualizacji są wykonywane na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="d1773-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="d1773-352">Rozwiązywanie konfliktów: powitalne SDK wykrywa zmiany powodujące konflikt zostały wprowadzone na powitania serwera i zawiera przechwytuje tooalert hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d1773-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="d1773-353">Usuwania nietrwałego: Usunięte rekordy są oznaczane usuniętych, dzięki czemu inne tooupdate urządzeń pamięci podręcznej w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="d1773-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="d1773-354">Inicjowanie synchronizacji w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="d1773-354">Initialize Offline Sync</span></span>

<span data-ttu-id="d1773-355">Każda tabela w trybie offline, musi być zdefiniowana w pamięci podręcznej offline hello przed użyciem.</span><span class="sxs-lookup"><span data-stu-id="d1773-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="d1773-356">Zwykle definicji tabeli odbywa się natychmiast po utworzeniu hello powitania klienta:</span><span class="sxs-lookup"><span data-stu-id="d1773-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="d1773-357">Uzyskaj odwołanie toohello w trybie Offline tabeli pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="d1773-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="d1773-358">Dla tabeli online, możesz użyć `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="d1773-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="d1773-359">Do tabeli w trybie offline, należy użyć `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="d1773-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="d1773-360">Witaj wszystkie dostępne metody online tabel (w tym filtrowania, sortowania, stronicowania, wstawiania danych, aktualizowanie danych i usunięcie danych) działa równie dobrze nadaje się do tabel w trybie online i jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="d1773-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="d1773-361">Synchronizuj hello lokalnej pamięci podręcznej trybu Offline</span><span class="sxs-lookup"><span data-stu-id="d1773-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="d1773-362">Synchronizacja jest w formancie hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="d1773-363">Oto przykład metody synchronizacji:</span><span class="sxs-lookup"><span data-stu-id="d1773-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="d1773-364">Jeśli nazwa zapytania jest dostarczany toohello `.pull(query, queryname)` metody, a następnie synchronizacja przyrostowa jest tooreturn używanych tylko rekordy, które zostały utworzone lub zmienione w stosunku do ściągania hello ostatnia zakończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="d1773-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="d1773-365">Obsługa konflikty podczas synchronizacji w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="d1773-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="d1773-366">Jeśli wystąpi konflikt podczas `.push()` operacji `MobileServiceConflictException` jest generowany.</span><span class="sxs-lookup"><span data-stu-id="d1773-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="d1773-367">Element wystawiony serwera Hello jest osadzony w hello wyjątku i mogą zostać pobrane przez `.getItem()` na powitania wyjątku.</span><span class="sxs-lookup"><span data-stu-id="d1773-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="d1773-368">Dostosuj wypychania hello przez wywołanie hello następujących elementów w obiekcie MobileServiceSyncContext hello:</span><span class="sxs-lookup"><span data-stu-id="d1773-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="d1773-369">Gdy wszystkie konflikty zostały oznaczone jako mają, wywołaj `.push()` ponownie tooresolve hello wszystkie konflikty.</span><span class="sxs-lookup"><span data-stu-id="d1773-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="d1773-370"><a name="custom-api"></a>Wywołaj niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d1773-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="d1773-371">Niestandardowy interfejs API umożliwia toodefine niestandardowe punkty końcowe, które udostępniają funkcje serwera które nie mapy tooan insert, update, usuwania lub operacja odczytu.</span><span class="sxs-lookup"><span data-stu-id="d1773-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="d1773-372">Przy użyciu niestandardowego interfejsu API, może mieć większą kontrolę nad wiadomości, w tym odczytywanie ustawienie nagłówki komunikatów HTTP i Definiowanie formatu treści wiadomości innych niż JSON.</span><span class="sxs-lookup"><span data-stu-id="d1773-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="d1773-373">Na kliencie z systemem Android należy wywołać hello **invokeApi** metody toocall hello niestandardowego interfejsu API punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d1773-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="d1773-374">Witaj poniższy przykład przedstawia sposób toocall interfejsu API punktu końcowego o nazwie **completeAll**, który zwraca klasę kolekcji o nazwie **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="d1773-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="d1773-375">Witaj **invokeApi** metoda jest wywoływana na powitania klienta, który wysyła ogłoszenie (POST) żądania toohello nowego niestandardowego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d1773-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="d1773-376">Witaj wynik zwracany przez hello niestandardowego interfejsu API jest wyświetlany w oknie dialogowym komunikatu, jak są błędy.</span><span class="sxs-lookup"><span data-stu-id="d1773-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="d1773-377">Inne wersje **invokeApi** można opcjonalnie Wysyłanie obiektu w treści żądania hello, określ metodę hello HTTP i Wyślij parametry zapytania z żądaniem hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="d1773-378">Bez typu wersje **invokeApi** znajdują się również.</span><span class="sxs-lookup"><span data-stu-id="d1773-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="d1773-379"><a name="authentication"></a>Dodaj aplikację tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="d1773-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="d1773-380">Samouczki już opisano szczegółowo sposób tooadd te funkcje.</span><span class="sxs-lookup"><span data-stu-id="d1773-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="d1773-381">Usługa aplikacji obsługuje [uwierzytelnianie użytkowników aplikacji](app-service-mobile-android-get-started-users.md) przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account, Twitter i Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1773-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="d1773-382">Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d1773-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="d1773-383">Umożliwia także tożsamości hello reguł autoryzacji tooimplement uwierzytelnionych użytkowników w sieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="d1773-384">Obsługiwane są dwa przepływy uwierzytelniania: **serwera** przepływu i **klienta** przepływu.</span><span class="sxs-lookup"><span data-stu-id="d1773-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="d1773-385">powitania serwera przepływu zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu sieci web dostawcy tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="d1773-386">Nie dodatkowe zestawy SDK są wymagane tooimplement serwera przepływ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d1773-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="d1773-387">Uwierzytelnianie serwera przepływu nie głęboką integrację hello urządzeń przenośnych i jest zalecane tylko dla dowód scenariuszy koncepcji.</span><span class="sxs-lookup"><span data-stu-id="d1773-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="d1773-388">powitania klienta przepływ umożliwia lepszą integrację z możliwości specyficznych dla urządzeń, takich jak logowanie jednokrotne zależy od udostępniane przez dostawcę tożsamości hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="d1773-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="d1773-389">Na przykład można zintegrować hello Facebook zestawu SDK aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="d1773-390">powitania klienta mobilnego zamienia do aplikacji usługi Facebook hello i sprawdza z logowania jednokrotnego przed wymiany wstecz tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="d1773-391">Cztery kroki są wymagane tooenable uwierzytelniania w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="d1773-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="d1773-392">Rejestrowanie aplikacji do uwierzytelniania przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="d1773-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="d1773-393">Skonfiguruj z wewnętrzną bazą danych z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="d1773-394">Ogranicz użytkowników tooauthenticated uprawnienia tabeli tylko na powitania wewnętrznej bazy danych z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="d1773-395">Dodaj aplikację tooyour kod uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d1773-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="d1773-396">Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d1773-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="d1773-397">Można również użyć hello identyfikator SID użytkownika uwierzytelnionego toomodify żądań.</span><span class="sxs-lookup"><span data-stu-id="d1773-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="d1773-398">Aby uzyskać więcej informacji, przejrzyj [Rozpoczynanie pracy z uwierzytelnianiem] i hello dokumentacji Porada zestawu SDK serwera.</span><span class="sxs-lookup"><span data-stu-id="d1773-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="d1773-399"><a name="caching"></a>Uwierzytelniania: Przepływ serwera</span><span class="sxs-lookup"><span data-stu-id="d1773-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="d1773-400">Witaj następujący kod uruchamia proces logowania przepływu serwera przy użyciu dostawcy Google hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="d1773-401">Ze względu na wymagania zabezpieczeń hello dostawcy Google hello jest wymagana dodatkowa konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="d1773-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="d1773-402">Ponadto Dodaj powitania po klasie działania głównego — metoda toohello:</span><span class="sxs-lookup"><span data-stu-id="d1773-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="d1773-403">Hello `GOOGLE_LOGIN_REQUEST_CODE` zdefiniowane w głównym Twojego to działanie służy do hello `login()` — metoda i w obrębie hello `onActivityResult()` metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="d1773-404">Można wybrać dowolny unikatowy numer, tak długo, jak hello sam numer jest używany w ramach hello `login()` — metoda i hello `onActivityResult()` metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="d1773-405">Jeśli kod klienta hello jest abstrakcyjny karty service (jak pokazano wcześniej), należy wywołać hello odpowiednie metody hello usługi karty.</span><span class="sxs-lookup"><span data-stu-id="d1773-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="d1773-406">Należy również tooconfigure hello projektu dla customtabs.</span><span class="sxs-lookup"><span data-stu-id="d1773-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="d1773-407">Najpierw określ URL przekierowania.</span><span class="sxs-lookup"><span data-stu-id="d1773-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="d1773-408">Dodaj powitania po fragment zbyt`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="d1773-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="d1773-409">Dodaj hello **redirectUriScheme** toohello `build.gradle` plików dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="d1773-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="d1773-410">Na koniec należy dodać `com.android.support:customtabs:23.0.1` toohello listę zależności w hello `build.gradle` pliku:</span><span class="sxs-lookup"><span data-stu-id="d1773-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="d1773-411">Uzyskać identyfikator hello hello zalogowanego użytkownika z **MobileServiceUser** przy użyciu hello **metodę getUserId** metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="d1773-412">Na przykład jak toocall prognoz toouse hello asynchroniczne logowania interfejsów API, zobacz [Rozpoczynanie pracy z uwierzytelnianiem].</span><span class="sxs-lookup"><span data-stu-id="d1773-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="d1773-413">Schemat adresów URL wymienionych Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d1773-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="d1773-414">Upewnij się, że wszystkie wystąpienia `{url_scheme_of_you_app}` wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d1773-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="d1773-415"><a name="caching"></a>Tokeny uwierzytelniania pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="d1773-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="d1773-416">Buforowanie tokeny uwierzytelniania wymaga hello toostore identyfikator użytkownika i token uwierzytelniania lokalnie na powitania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d1773-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="d1773-417">Witaj następnym uruchomieniu aplikacji hello sprawdzania hello pamięci podręcznej, a jeśli te wartości są obecne, możesz pominąć dziennika hello w procedurze i rehydrate powitania klienta przy użyciu tych danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="d1773-418">Jednak te dane są poufne i powinny być przechowywane, szyfrowane ze względów bezpieczeństwa w przypadku kradzieży hello telefonu.</span><span class="sxs-lookup"><span data-stu-id="d1773-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="d1773-419">Widać pełny przykład sposobu uwierzytelniania toocache tokenów w [pamięci podręcznej sekcji tokeny uwierzytelniania][7].</span><span class="sxs-lookup"><span data-stu-id="d1773-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="d1773-420">Podczas próby toouse wygasły token pojawi się *401 nieautoryzowane* odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d1773-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="d1773-421">Może obsługiwać błędy uwierzytelniania za pomocą filtrów.</span><span class="sxs-lookup"><span data-stu-id="d1773-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="d1773-422">Filtry przechwycić toohello żądań aplikacji usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1773-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="d1773-423">Kod filtru Hello testów hello odpowiedzi 401, wyzwala hello procesu logowania i zostanie wznowiony hello żądania, który wygenerował hello 401.</span><span class="sxs-lookup"><span data-stu-id="d1773-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="d1773-424"><a name="refresh"></a>Używaj tokenów odświeżania</span><span class="sxs-lookup"><span data-stu-id="d1773-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="d1773-425">token Hello zwracany przez usługi Azure App Service uwierzytelniania i autoryzacji ma zdefiniowany czas jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="d1773-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="d1773-426">Po tym okresie ponownego uwierzytelnienia użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="d1773-427">W przypadku tego samego tokenu hello z usługi Azure App Service Authentication przy użyciu długotrwałe token, który ma odebranych za pośrednictwem uwierzytelniania przepływu klienta, a następnie można ponownego uwierzytelnienia i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="d1773-428">Inny token usługi Azure App Service jest generowany nowy okres istnienia.</span><span class="sxs-lookup"><span data-stu-id="d1773-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="d1773-429">Można również zarejestrować hello toouse dostawcy tokenów odświeżania.</span><span class="sxs-lookup"><span data-stu-id="d1773-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="d1773-430">Token odświeżania nie zawsze jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="d1773-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="d1773-431">Wymagana jest dodatkowa konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="d1773-431">Additional configuration is required:</span></span>

* <span data-ttu-id="d1773-432">Aby uzyskać **usługi Azure Active Directory**, skonfiguruj klucz tajny klienta na powitania aplikacji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1773-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="d1773-433">Określ klucz tajny klienta hello hello Azure App Service, podczas konfigurowania uwierzytelniania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1773-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="d1773-434">Podczas wywoływania metody `.login()`, Przekaż `response_type=code id_token` jako parametr:</span><span class="sxs-lookup"><span data-stu-id="d1773-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="d1773-435">Aby uzyskać **Google**, Przekaż hello `access_type=offline` jako parametr:</span><span class="sxs-lookup"><span data-stu-id="d1773-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="d1773-436">Aby uzyskać **Account Microsoft**, wybierz pozycję hello `wl.offline_access` zakresu.</span><span class="sxs-lookup"><span data-stu-id="d1773-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="d1773-437">Wywołanie toorefresh token, `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="d1773-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="d1773-438">Najlepszym rozwiązaniem utworzyć filtr, który wykryje 401 odpowiedzi z serwera hello i próbuje toorefresh hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="d1773-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="d1773-439">Zaloguj się przy użyciu uwierzytelniania przepływu klienta</span><span class="sxs-lookup"><span data-stu-id="d1773-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="d1773-440">Witaj ogólny proces logowania się za pomocą klienta przepływ uwierzytelniania wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d1773-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="d1773-441">Konfigurowanie usługi Azure App Service uwierzytelniania i autoryzacji, jak w przypadku uwierzytelniania serwera przepływu.</span><span class="sxs-lookup"><span data-stu-id="d1773-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="d1773-442">Integracja hello dostawcy uwierzytelniania zestawu SDK dla uwierzytelniania tooproduce tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d1773-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="d1773-443">Wywołaj hello `.login()` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d1773-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="d1773-444">Zastąp hello `onSuccess()` metody z dowolnym kod ma toouse na pomyślnego logowania.</span><span class="sxs-lookup"><span data-stu-id="d1773-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="d1773-445">Witaj `{provider}` ciąg jest prawidłowym dostawcą: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, lub **twitter**.</span><span class="sxs-lookup"><span data-stu-id="d1773-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="d1773-446">Jeśli zaimplementowano niestandardowe uwierzytelnianie, można również użyć hello uwierzytelniania niestandardowego dostawcy tagu.</span><span class="sxs-lookup"><span data-stu-id="d1773-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="d1773-447"><a name="adal"></a>Uwierzytelnianie użytkowników z hello Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="d1773-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="d1773-448">Witaj Active Directory Authentication Library (ADAL) toosign użytkowników służy do aplikacji przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1773-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="d1773-449">Przy użyciu identyfikatora logowania przepływu klienta jest często hello preferowane toousing `loginAsync()` metody, ponieważ zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="d1773-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d1773-450">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD przez następujące hello [jak tooconfigure aplikacji usługi dla usługi Active Directory logowania] [ 22] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d1773-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="d1773-451">Upewnij się, że toocomplete hello opcjonalny krok rejestrowania aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="d1773-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="d1773-452">Zainstaluj biblioteki ADAL, modyfikując Twojej hello tooinclude plik build.gradle następujące definicje:</span><span class="sxs-lookup"><span data-stu-id="d1773-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="d1773-453">Dodaj hello następującego kodu tooyour aplikacji, przez co hello następujące elementy zastępcze:</span><span class="sxs-lookup"><span data-stu-id="d1773-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="d1773-454">Zastąp **INSERT urzędu tutaj** o nazwie hello hello dzierżawy, w którym są udostępniane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="d1773-455">https://login.microsoftonline.com/contoso.onmicrosoft.com powinna mieć ona Hello format.</span><span class="sxs-lookup"><span data-stu-id="d1773-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="d1773-456">Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta powitania dla zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="d1773-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="d1773-457">Identyfikator klienta hello można uzyskać z hello **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="d1773-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="d1773-458">Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta hello skopiowany z hello aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="d1773-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="d1773-459">Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d1773-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="d1773-460">Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="d1773-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="d1773-461"><a name="filters"></a>Dostosuj hello komunikacji klient-serwer</span><span class="sxs-lookup"><span data-stu-id="d1773-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="d1773-462">Witaj połączenie klienta jest zwykle podstawowe połączenie HTTP przy użyciu hello podstawowej biblioteki HTTP dostarczony wraz z hello zestawu SDK systemu Android.</span><span class="sxs-lookup"><span data-stu-id="d1773-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="d1773-463">Istnieje kilka przyczyn, dlaczego warto toochange który:</span><span class="sxs-lookup"><span data-stu-id="d1773-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="d1773-464">Chcesz toouse alternatywny HTTP biblioteki tooadjust przekroczeń limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="d1773-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="d1773-465">Chcesz tooprovide pasek postępu.</span><span class="sxs-lookup"><span data-stu-id="d1773-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="d1773-466">Chcesz tooadd z funkcji zarządzania toosupport interfejsu API niestandardowego nagłówka.</span><span class="sxs-lookup"><span data-stu-id="d1773-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="d1773-467">Chcesz toointercept odpowiedzi nie powiodło się, aby zaimplementować ponowne uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="d1773-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="d1773-468">Chcesz, aby usługa analiza tooan toolog wewnętrznej bazy danych żądania.</span><span class="sxs-lookup"><span data-stu-id="d1773-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="d1773-469">Za pomocą alternatywnej biblioteki HTTP</span><span class="sxs-lookup"><span data-stu-id="d1773-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="d1773-470">Wywołaj hello `.setAndroidHttpClientFactory()` metody natychmiast po utworzeniu odwołanie do klienta.</span><span class="sxs-lookup"><span data-stu-id="d1773-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="d1773-471">Na przykład tooset hello połączenia too60 liczba sekund limitu czasu (zamiast domyślnego hello 10 sekund):</span><span class="sxs-lookup"><span data-stu-id="d1773-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="d1773-472">Implementuje filtr postępu</span><span class="sxs-lookup"><span data-stu-id="d1773-472">Implement a Progress Filter</span></span>

<span data-ttu-id="d1773-473">ODCIĘTA każde żądanie można zaimplementować zaimplementowanie `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="d1773-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="d1773-474">Na przykład następujące hello aktualizuje pasek postępu wstępnie utworzone:</span><span class="sxs-lookup"><span data-stu-id="d1773-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="d1773-475">Możesz dołączyć ten klient toohello filtru w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d1773-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="d1773-476">Dostosowywanie nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="d1773-476">Customize Request Headers</span></span>

<span data-ttu-id="d1773-477">Użyj następujących hello `ServiceFilter` i Dołącz filtr hello w hello tak samo jak hello `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="d1773-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="d1773-478"><a name="conversions"></a>Skonfiguruj automatyczne serializacji</span><span class="sxs-lookup"><span data-stu-id="d1773-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="d1773-479">Można określić strategii konwersji, która ma zastosowanie tooevery kolumny za pomocą hello [gson] [ 3] interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d1773-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="d1773-480">Biblioteka klienta dla systemu Android Hello używa [gson] [ 3] tle hello tooserialize Java obiekty tooJSON danych przed wysłaniem danych hello tooAzure usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1773-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="d1773-481">Witaj poniższy kod używa hello **setFieldNamingStrategy()** strategii hello tooset metody.</span><span class="sxs-lookup"><span data-stu-id="d1773-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="d1773-482">W tym przykładzie spowoduje usunięcie hello początkowy znak ("m"), a następnie małe hello następny znak, dla każdej nazwy pola.</span><span class="sxs-lookup"><span data-stu-id="d1773-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="d1773-483">Na przykład go spowoduje przekształcenie "mId" w "id".</span><span class="sxs-lookup"><span data-stu-id="d1773-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="d1773-484">Implementowanie potrzebę hello tooreduce strategii konwersji `SerializedName()` adnotacje w większości pól.</span><span class="sxs-lookup"><span data-stu-id="d1773-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="d1773-485">Ten kod musi zostać wykonana przed utworzeniem odwołanie klientów urządzeń przenośnych przy użyciu hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="d1773-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Rozpoczynanie pracy z uwierzytelnianiem]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
