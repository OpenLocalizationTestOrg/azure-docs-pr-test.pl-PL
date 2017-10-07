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
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Jak toouse hello Azure Mobile Apps SDK dla systemu Android

Ten przewodnik przedstawia, jak toouse hello kliencką dla systemu Android SDK dla typowych scenariuszy tooimplement Mobile Apps, takich jak:

* Wyszukiwanie danych (wstawiania, aktualizowania i usuwania).
* Uwierzytelnianie.
* Obsługa błędów.
* Dostosowywanie powitania klienta.

Ten przewodnik koncentruje się na powitania klienta zestawu SDK systemu Android.  więcej informacji o toolearn hello zestawów SDK po stronie serwera dla Mobile Apps, zobacz [pracować z zaplecza .NET SDK] [ 10] lub [jak toouse hello zaplecza Node.js SDK] [ 11].

## <a name="reference-documentation"></a>Dokumentacji

Można znaleźć hello [dokumentacja interfejsu API Javadocs] [ 12] hello biblioteki klienta dla systemu Android w witrynie GitHub.

## <a name="supported-platforms"></a>Obsługiwane platformy

Hello Azure Mobile Apps SDK dla systemu Android obsługuje poziom interfejsu API 19 do 24 (KitKat za pośrednictwem nugacie) Telefon i tablet rozmiarach.  Korzysta z uwierzytelniania, w szczególności wspólnej poświadczeń toogather podejście framework sieci web.  Uwierzytelnianie serwera przepływu nie działa z niewielkich współczynnik urządzeń, takich jak obserwowanie.

## <a name="setup-and-prerequisites"></a>Instalacji i wymagania wstępne

Zakończenie hello [szybkiego startu Mobile Apps](app-service-mobile-android-get-started.md) samouczka.  To zadanie gwarantuje, że zostały spełnione wszystkie wymagania wstępne związane z opracowywaniem Azure Mobile Apps.  Witaj szybkiego startu pomaga również skonfigurować konta i utworzyć pierwszy zaplecza aplikacji mobilnej.

Jeśli zdecydujesz się nie toocomplete samouczek Szybki Start — Witaj, wykonaj hello następujące zadania:

* [Tworzenie zaplecza aplikacji mobilnej] [ 13] toouse z aplikacji systemu Android.
* W programie Android Studio [hello aktualizacji Gradle kompilacja plików](#gradle-build).
* [Włącz uprawnień internetowych](#enable-internet).

### <a name="gradle-build"></a>Aktualizacja hello Gradle kompilacji pliku

Zmiana obu **build.gradle** plików:

1. Dodaj ten kod toohello *projektu* poziom **build.gradle** pliku wewnątrz hello *buildscript* tagu:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Dodaj ten kod toohello *aplikacji modułu* poziom **build.gradle** pliku wewnątrz hello *zależności* tagu:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Najnowsza wersja hello jest obecnie 3.3.0. Witaj obsługiwane wersje są wymienione [w serwisie bintray][14].

### <a name="enable-internet"></a>Włącz uprawnień internetowych

tooaccess Azure aplikacji musi mieć włączone uprawnienia INTERNET hello. Jeśli nie zostało jeszcze jest włączone, należy dodać powitania po wierszu kodu tooyour **AndroidManifest.xml** pliku:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Utwórz połączenie klienta

Azure Mobile Apps udostępnia cztery funkcje tooyour aplikacji mobilnej:

* Dostęp do danych i synchronizacji z usługą Azure Mobile Services aplikacje w trybie Offline.
* Wywoływania niestandardowych interfejsów API napisany za pomocą hello zestaw SDK usługi Azure Mobile Apps serwera.
* Uwierzytelnianie za pomocą usługi aplikacji Azure uwierzytelniania i autoryzacji.
* Rejestracja powiadomień z koncentratorami powiadomień wypychanych.

Każda z tych funkcji wymaga najpierw utworzenia `MobileServiceClient` obiektu.  Tylko jeden `MobileServiceClient` obiekt powinien zostać utworzony w ramach sieci klientów urządzeń przenośnych (to znaczy, należy go wzorzec Singleton).  toocreate `MobileServiceClient` obiektu:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Witaj `<MobileAppUrl>` to ciąg lub obiekt adres URL, który wskazuje tooyour zaplecze aplikacji mobilnej.  Jeśli używasz usługi Azure App Service toohost z zaplecza aplikacji mobilnych, upewnij się, użyj hello bezpiecznego `https://` wersji hello adresu URL.

powitania klienta wymaga również toohello dostępu działania lub kontekstu — Witaj `this` parametru w przykładzie hello.  Hello konstrukcji MobileServiceClient powinno się zdarzyć w hello `onCreate()` metody hello w hello odwoływać się działanie `AndroidManifest.xml` pliku.

Jako najlepsze rozwiązanie należy abstrakcyjnej komunikacji z serwerem do własnej klasy (wzorca singleton).  W takim przypadku należy przekazać hello działania w ramach tooappropriately Konstruktor hello skonfigurować usługę hello.  Na przykład:

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

Można teraz wywołać `AzureServiceAdapter.Initialize(this);` w hello `onCreate()` metody działania głównego.  Użyj innych metod wymagające dostępu klienta toohello `AzureServiceAdapter.getInstance();` tooobtain karty usługi toohello odwołania.

## <a name="data-operations"></a>Operacje na danych

Hello najważniejsza część hello Azure Mobile Apps SDK jest toodata dostępu tooprovide przechowywane w ramach usług SQL Azure na powitania zaplecza aplikacji mobilnej.  Można uzyskać dostępu do te dane przy użyciu klasy jednoznacznie (preferowane) lub wykonywania kwerend (niezalecane).  zbiorcze Hello przedstawione w tej sekcji zajmuje się przy użyciu silnie typizowanej klasy.

### <a name="define-client-data-classes"></a>Definiowanie klas danych klienta

tooaccess dane z tabel SQL Azure, definiowania klas danych klienta, które odpowiadają toohello tabel w hello zaplecza aplikacji mobilnej. Przykłady w tym temacie założono tabela o nazwie **MyDataTable**, która zawiera następujące kolumny hello:

* id
* Tekst
* Zakończenie

Witaj odpowiedni obiekt typu po stronie klienta znajduje się w pliku o nazwie **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Dodaj metody pobierającej i ustawiającej dla każdego pola, które można dodać.  Jeśli tabela SQL Azure zawiera więcej kolumn, należy dodać hello odpowiadającą klasę toothis pola.  Na przykład, jeśli hello DTO kolumna priorytet liczb całkowitych miał (obiektu transferu danych), a następnie można dodać tego pola, wraz z jego metody pobierającej i ustawiającej:

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

toolearn toocreate dodatkowe tabele w zapleczu swojej Mobile Apps, zobacz temat [porady: Definiowanie kontrolera tabeli] [ 15] (zaplecze .NET) lub [zdefiniuj tabel za pomocą dynamicznej schematu] [ 16] (Zaplecza Node.js).

Azure Mobile Apps tabeli wewnętrznej bazy danych definiuje pięć specjalne pól, z których cztery są dostępne tooclients:

* `String id`: hello globalnie unikatowy identyfikator hello rekordu.  Jako najlepsze rozwiązanie należy hello identyfikator hello reprezentację ciągu [UUID] [ 17] obiektu.
* `DateTimeOffset updatedAt`: hello Data/godzina ostatniej aktualizacji hello.  Witaj updatedAt pola jest ustawiana przez powitania serwera i nie powinno być używane przez kod klienta.
* `DateTimeOffset createdAt`: hello daty i godziny utworzenia tego obiektu hello.  Witaj createdAt pola jest ustawiana przez powitania serwera i nie powinno być używane przez kod klienta.
* `byte[] version`: Zazwyczaj reprezentowany jako ciąg, wersja hello jest również ustawić powitania serwera.
* `boolean deleted`: Wskazuje, że rekord hello została usunięta, ale nie są przeczyszczane jeszcze.  Nie używaj `deleted` jako właściwość w klasie.

Witaj `id` pole jest wymagane.  Witaj `updatedAt` pola i `version` pola są używane do synchronizacji w trybie offline (przyrostowej synchronizacji i wystąpi konflikt rozpoznawania odpowiednio).  Witaj `createdAt` pole jest polem Odwołanie i nie jest używana przez powitania klienta.  nazwy Hello "w locie" nazwy właściwości hello i nie są zmieniane.  Jednak można utworzyć mapowania między obiektu i hello "w locie" nazw przy użyciu hello [gson] [ 3] biblioteki.  Na przykład:

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

### <a name="create-a-table-reference"></a>Tworzenie odwołania do tabeli

tooaccess tabeli, najpierw utwórz [MobileServiceTable] [ 8] obiektu wywołującego hello **getTable** metody na powitania [MobileServiceClient][9].  Ta metoda ma dwa przeciążenia:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

W hello następującego kodu **mClient** jest obiektem MobileServiceClient tooyour odwołania.  przeciążenia pierwszy Hello jest używany, gdzie hello nazwę klasy i nazwę tabeli hello są hello takie same i hello jeden służy w hello Szybki Start:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Witaj przeciążenia drugi jest używany podczas hello Nazwa tabeli jest inna niż nazwa klasy hello: hello pierwszym parametrem jest hello nazwy tabeli.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Zapytania dotyczącego tabeli wewnętrznej bazy danych

Najpierw należy uzyskać odwołania do tabeli.  Następnie można wykonać zapytania na powitania odwołanie do tabeli.  Zapytanie jest dowolną kombinację:

* A `.where()` [klauzuli filtru](#filtering).
* `.orderBy()` [Porządkowanie klauzuli](#sorting).
* A `.select()` [pola wyboru klauzuli](#selection).
* A `.skip()` i `.top()` dla [stronicowanej wyniki](#paging).

klauzule Hello przedstawia w hello poprzedzających kolejności.

### <a name="filter"></a>Filtrowanie wyników

Formularz ogólny Hello zapytania jest:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Witaj poprzedni przykład zwraca wszystkie wyniki (up toohello maksymalny rozmiar strony ustawione przez powitania serwera).  Witaj `.execute()` metoda wykonuje zapytanie hello hello wewnętrznej bazy danych.  Hello zapytanie jest przekonwertowanego tooan [OData v3] [ 19] zapytania przed transmisji toohello Mobile Apps wewnętrznej bazy danych.  Po otrzymaniu zaplecza aplikacji mobilnej hello konwertuje hello zapytania do instrukcji SQL przed jej wykonanie w wystąpieniu SQL Azure hello.  Ponieważ działania sieci dopiero po pewnym czasie, hello `.execute()` metoda zwraca [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Filtr zwrócił danych

powitania po wykonywania zapytania zwraca wszystkie elementy z hello **ToDoItem** tabeli where **pełną** jest równe **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** jest hello odwołanie toohello usługi mobilnej tabeli utworzonej wcześniej.

Zdefiniuj filtr przy użyciu hello **gdzie** wywołanie metody hello w odwołaniu do tabeli. Witaj **gdzie** następuje — metoda **pola** metody następuje metodę, która określa hello logicznej predykatu. Predykatu metod uwzględnić **eq** (równe), **ne** (nie równa), **gt** (większe niż) **ge** (większe lub równe), **lt** (poniżej), **le** (mniejsze niż lub równe). Te metody umożliwiają porównanie liczby i toospecific wartości w polach ciąg.

Można filtrować według daty. Hello następujące metody umożliwiają porównanie hello Data całego lub części daty hello: **roku**, **miesiąca**, **dzień**, **godzinę**, **minutę**, i **drugi**. Witaj poniższy przykład umożliwia dodanie filtru dla elementów których *termin* jest równe 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Witaj następujących metod obsługi złożonych filtrów na pól ciągów: **startsWith**, **endsWith**, **concat**, **podciąg**, **indexOf**, **Zastąp**, **toLower**, **toUpper**, **trim**, i  **długość**. następujące przykładowe filtry dla tabeli wiersze, w których hello Hello *tekst* kolumny rozpoczyna się od "PRI0."

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

następujące metody operator Hello są obsługiwane w pola liczb: **dodać**, **sub**, **mul**, **div**, **mod**, **floor**, **limitu**, i **zaokrąglona**. następujące przykładowe filtry dla tabeli wiersze, w których hello Hello **czas trwania** jest liczbą parzystą.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

Predykaty można połączyć z tych metod logiczne: **i**, **lub** i **nie**. Poniższy przykład Hello łączy dwa hello poprzedzających przykłady.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Operatory logiczne grupy i gniazda:

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

Aby uzyskać bardziej szczegółowe omówienie i przykłady filtrowania, zobacz [eksploracji siłę hello powitania klienta dla systemu Android zapytania modelu][20].

### <a name="sorting"></a>Sortowanie zwrócone dane

Witaj następujący kod zwraca wszystkie elementy z tabeli z **ToDoItems** sortowane rosnąco przez hello *tekst* pola. *mToDoTable* jest hello toohello zaplecza spis utworzonego wcześniej:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

pierwszy parametr hello Hello **orderBy** — metoda jest nazwą równy toohello ciąg hello pola, w których toosort. drugi parametr Hello używa hello **QueryOrder** toospecify wyliczenie czy toosort w kolejności rosnącej lub malejącej.  Jeśli są filtrowanie przy użyciu hello ***gdzie*** metoda, hello ***gdzie*** metody należy wywołać przed hello ***orderBy*** — metoda.

### <a name="selection"></a>Wybrać określone kolumny

Hello poniższy kod ilustruje sposób tooreturn wszystkich elementów z tabeli **ToDoItems**, ale wyświetlane są tylko hello **pełną** i **tekst** pola. **mToDoTable** jest hello odwołanie toohello zaplecza tabeli utworzonej wcześniej.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

Funkcja wybierz toohello parametry Hello są nazwami ciąg hello hello tabeli kolumn, które mają tooreturn.  Witaj **wybierz** metody musi toofollow metody, takie jak **gdzie** i **orderBy**. Może występować przez metody stronicowania, takie jak **pominąć** i **górnej**.

### <a name="paging"></a>Zwróć dane strony

Dane są **zawsze** zwracane w stronach.  Witaj maksymalną liczbę rekordów zwróconych jest ustawiana przez serwer hello.  Jeśli powitania klienta żąda więcej rekordów, powitania serwera zwraca hello maksymalną liczbę rekordów.  Domyślnie program hello maksymalny rozmiar strony na powitania serwera jest 50 rekordów.

Hello pierwszym przykładzie pokazano, jak tooselect hello pierwsze pięć elementy z tabeli. Hello zapytanie zwraca hello elementów z tabeli z **ToDoItems**. **mToDoTable** jest hello toohello zaplecza spis utworzonego wcześniej:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Oto zapytania, że pomija hello pięć pierwszych elementów, a następnie zwraca hello następnych pięciu:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Jeśli chcesz tooget wszystkie rekordy w tabeli, należy zaimplementować tooiterate kodu za pośrednictwem wszystkich stron:

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

Żądanie dla wszystkich rekordów za pomocą tej metody tworzy co najmniej dwa żądania toohello Mobile Apps wewnętrznej bazy danych.

> [!TIP]
> Wybieranie rozmiaru prawej strony hello jest kompromis między użycia pamięci podczas żądania hello jest wykonywane, przepustowości i opóźnień w całkowicie odbieranie danych hello.  domyślne Hello (50 rekordów) jest odpowiednia dla wszystkich urządzeń.  Wyłącznie w przypadku obsługi większych urządzeń pamięci, należy zwiększyć się too500.  Znaleziono ten zwiększa rozmiar strony hello ponad 500 rejestruje wyniki nie do przyjęcia opóźnienia i problemy z dużej ilości pamięci.

### <a name="chaining"></a>Porady: łączenie metody zapytania

może zostać dołączona metody Hello badania tabel wewnętrznej bazy danych. Tworzenie łańcuchów metody umożliwia tooselect określonych kolumn filtrowane wierszy, które są sortowane i stronicowane zapytanie. Można tworzyć złożone filtry logiczne.  Każda metoda zapytanie zwraca obiekt zapytania. ciąg hello tooend metod i hello faktycznie wykonywania zapytania, wywołanie hello **wykonania** metody. Na przykład:

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

Witaj powiązane zapytania metody muszą być uporządkowane w następujący sposób:

1. Filtrowanie (**gdzie**) metod.
2. Sortowanie (**orderBy**) metod.
3. Wybór (**wybierz**) metod.
4. stronicowanie (**pominąć** i **górnej**) metod.

## <a name="binding"></a>Powiąż interfejsu użytkownika toohello danych

Powiązanie danych obejmuje trzy składniki:

* Witaj źródła danych
* Witaj układu ekranu
* Karta Hello czy ties Witaj dwie razem.

W naszym przykładowym kodzie hello danych zwróconych z tabeli Mobile Apps SQL Azure hello **ToDoItem** do tablicy. To działanie jest wspólnego wzorca dla danych aplikacji.  Zapytania bazy danych często zwracać kolekcji wierszy, które hello klient pobiera listy lub tablicy. W tym przykładzie tablica hello jest hello źródła danych.  Kod Hello określa układ ekranu, definiujący widok hello hello dane wyświetlane na urządzeniu hello.  Witaj dwie powiązanych wraz z karty, którego ten kod jest rozszerzeniem hello **ArrayAdapter&lt;ToDoItem&gt;**  klasy.

#### <a name="layout"></a>Zdefiniuj hello układu

Witaj układ jest definiowany przez kilka fragmentów kodu XML. Biorąc pod uwagę istniejącego układu, hello następującego kodu reprezentuje hello **ListView** chcemy toopopulate z naszych danych serwera.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

W hello poprzedzających kodu, hello *listitem* atrybut określa identyfikator hello hello układu dla pojedynczego wiersza na liście hello. Ten kod pobiera utworzyć raz dla każdego elementu na liście hello i określa pole wyboru i jego tekst. Ten układ nie wyświetla hello **identyfikator** pola i bardziej złożonej układu określić dodatkowe pola hello wyświetlania. Ten kod jest hello **row_list_to_do.xml** pliku.

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

#### <a name="adapter"></a>Zdefiniuj hello karty
Ponieważ źródło danych hello naszych widoku jest tablicą **ToDoItem**, możemy podklasy naszych karty z **ArrayAdapter&lt;ToDoItem&gt;**  klasy. To podklasa tworzy widok dla każdego **ToDoItem** przy użyciu hello **row_list_to_do** układu.  W naszym kodzie zdefiniować następujące klasy, która jest rozszerzeniem hello hello **ArrayAdapter&lt;E&gt;**  klasy:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Zastąpienie kart hello **getView** metody. Na przykład:

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

Tworzymy wystąpienie tej klasy w naszych działań w następujący sposób:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Witaj drugi parametr toohello ToDoItemAdapter Konstruktor jest układ toohello odwołania. Firma Microsoft może teraz utworzyć wystąpienia hello **ListView** i przypisz hello karty toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Użyj hello karty tooBind toohello interfejsu użytkownika

Wszystko jest teraz gotowy toouse powiązania danych. Witaj poniższy kod przedstawia sposób tooget elementów w tabeli hello i wypełnienia hello karty lokalnej z hello zwracane elementy.

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

Wywołaj karty hello kiedykolwiek zmodyfikujesz hello **ToDoItem** tabeli. Ponieważ zmiany są wykonywane na podstawie rekordu na podstawie, można obsługiwać pojedynczy wiersz zamiast kolekcji. Po wstawieniu elementu wywołać hello **dodać** — metoda na hello karty; podczas usuwania, wywołaj hello **Usuń** — metoda.

Pełny przykład można znaleźć w hello [projektu szybkiego startu dla systemu Android][21].

## <a name="inserting"></a>Wstawianie danych do hello wewnętrznej bazy danych

Tworzy wystąpienie hello *ToDoItem* klasy i ustawienia swoich właściwości.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Następnie użyj **operacji insert()** tooinsert obiektu:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Hello zwrócił zgodne jednostki danych hello wstawione do tabeli wewnętrznej bazy danych hello, identyfikator hello dołączone i inne wartości (takie jak hello `createdAt`, `updatedAt`, i `version` pól) Ustaw hello wewnętrznej bazy danych.

Tabele Mobile Apps, wymagają kolumna klucza podstawowego o nazwie **identyfikator**. Ta kolumna musi być ciągiem. Wartość domyślna Hello hello identyfikator kolumny jest identyfikatorem GUID.  Możesz podać inne unikatowe wartości, takie jak adresy e-mail lub nazwy użytkowników. Nie podano wartość Identyfikatora ciągu wstawionego rekordu, zaplecza hello generuje nowy identyfikator GUID.

Ciąg Identyfikatora wartości zawierają hello następujące korzyści:

* Identyfikatory mogą być generowane bez wprowadzania toohello obiegu bazy danych.
* Rekordy są łatwiejsze toomerge z różnych tabel lub baz danych.
* Wartości Identyfikatora lepszą integrację z logiki aplikacji.

Ciąg Identyfikatora wartości są **REQUIRED** obsługę synchronizacji w trybie offline.  Nie można zmienić identyfikatora, gdy jest on przechowywany w hello wewnętrznej bazy danych.

## <a name="updating"></a>Aktualizuj dane w aplikacji mobilnej

tooupdate dane w tabeli, Przekaż hello nowy obiekt toohello **update()** metody.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

W tym przykładzie *elementu* jest odwołanie do wiersza tooa hello *ToDoItem* tabeli, które były tooit niektóre zmiany wprowadzone.  Hello wiersz z hello sam **identyfikator** jest aktualizowany.

## <a name="deleting"></a>Usuwanie danych w aplikacji mobilnej

Witaj następującego kodu pokazuje, jak toodelete danych z tabeli, określając hello obiektu danych.

```java
mToDoTable
    .delete(item);
```

Można również usunąć element, określając hello **identyfikator** pole hello toodelete wiersza.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Wyszukiwanie określonego elementu według identyfikatora

Wyszukiwanie elementu z określonym **identyfikator** pole z hello **lookUp()** metody:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Porady: Praca z danymi bez typu

model programowania bez typu Hello zapewnia dokładną kontrolę nad serializacji JSON.  Brak niektórych typowych scenariuszy, w którym możesz toouse model programowania bez typu. Na przykład, jeśli tabela wewnętrznej bazy danych zawiera wiele kolumn, wystarczy tooreference podzbiór hello kolumn.  model typu Hello wymaga toodefine wszystkich kolumn hello zdefiniowanych w hello zaplecza aplikacji mobilnej w klasie danych.  Większość hello wywołania interfejsu API w celu uzyskania dostępu do danych są podobne toohello wpisane wywołania programowania. Witaj podstawowa różnica polega na czy w modelu bez typu hello można wywołać metod w hello **MobileServiceJsonTable** obiektu zamiast hello **MobileServiceTable** obiektu.

### <a name="json_instance"></a>Utwórz wystąpienie tabeli bez typu

Podobne toohello wpisane modelu, możesz uruchomić pobierania odwołania do tabeli, ale w tym przypadku jest **MobileServicesJsonTable** obiektu. Uzyskaj odwołanie hello przez wywołanie hello **getTable** metody w wystąpieniu powitania klienta:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Po utworzeniu wystąpienia hello **MobileServiceJsonTable**, praktycznie ma tekst hello tego samego interfejsu API, które są dostępne jako z modelem programowania typu hello. W niektórych przypadkach hello metody przyjmują bez typu parametru zamiast parametru typu.

### <a name="json_insert"></a>Wstaw do tabeli bez typu
Witaj następującego kodu pokazuje sposób toodo insert. Witaj pierwszym krokiem jest toocreate [JsonObject][1], który jest częścią hello [gson] [ 3] biblioteki.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Następnie należy użyć **operacji insert()** tooinsert hello nieuwzględniające typów obiektów do tabeli hello.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Jeśli potrzebny jest identyfikator hello tooget hello wstawić obiektu, użyj hello **getAsJsonPrimitive()** metody.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Usuń z tabeli bez typu
Witaj poniższy kod przedstawia sposób toodelete instancję, w tym przypadku hello tego samego wystąpienia **JsonObject** utworzony we wcześniejszej hello *Wstaw* przykład. Kod Hello jest hello takie same jak w przypadku hello wpisane przypadek, ale metoda hello ma inny podpis, ponieważ odwołuje się on **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

Możesz także usunąć wystąpienia bezpośrednio za pomocą jego Identyfikatora:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Zwracanie wszystkich wierszy z tabeli bez typu
Witaj następującego kodu pokazuje sposób tooretrieve całej tabeli. Ponieważ używasz tabeli JSON, można selektywnie pobierać tylko niektóre kolumny tabeli hello.

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

Witaj tego samego zestawu filtrowania, filtrowania i stronicowania metod, które są dostępne dla modelu typu hello są dostępne dla hello bez typu modelu.

## <a name="offline-sync"></a>Implementowanie synchronizacji w trybie Offline

Witaj zestawu SDK klienta usługi Azure Mobile Apps implementuje również synchronizacji danych w trybie offline przy użyciu kopii danych serwera hello toostore bazy danych SQLite lokalnie.  Operacje wykonywane w trybie offline tabeli nie wymagają toowork łączność.  Synchronizacja w trybie offline pomaga odporności i wydajności na powitania koszt bardziej złożonej logiki do rozwiązywania konfliktów.  Witaj zestawu SDK klienta usługi Azure Mobile Apps implementuje hello następujące funkcje:

* Synchronizacja przyrostowa: Tylko zaktualizowanych i nowych rekordów są pobierane, zapisywanie zużycie przepustowości i pamięci.
* Optymistycznej współbieżności: Operacje są uznawane za toosucceed.  Rozwiązywanie konfliktów jest odłożona do aktualizacji są wykonywane na powitania serwera.
* Rozwiązywanie konfliktów: powitalne SDK wykrywa zmiany powodujące konflikt zostały wprowadzone na powitania serwera i zawiera przechwytuje tooalert hello użytkownika.
* Usuwania nietrwałego: Usunięte rekordy są oznaczane usuniętych, dzięki czemu inne tooupdate urządzeń pamięci podręcznej w trybie offline.

### <a name="initialize-offline-sync"></a>Inicjowanie synchronizacji w trybie Offline

Każda tabela w trybie offline, musi być zdefiniowana w pamięci podręcznej offline hello przed użyciem.  Zwykle definicji tabeli odbywa się natychmiast po utworzeniu hello powitania klienta:

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

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Uzyskaj odwołanie toohello w trybie Offline tabeli pamięci podręcznej

Dla tabeli online, możesz użyć `.getTable()`.  Do tabeli w trybie offline, należy użyć `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Witaj wszystkie dostępne metody online tabel (w tym filtrowania, sortowania, stronicowania, wstawiania danych, aktualizowanie danych i usunięcie danych) działa równie dobrze nadaje się do tabel w trybie online i jest w trybie offline.

### <a name="synchronize-hello-local-offline-cache"></a>Synchronizuj hello lokalnej pamięci podręcznej trybu Offline

Synchronizacja jest w formancie hello aplikacji.  Oto przykład metody synchronizacji:

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

Jeśli nazwa zapytania jest dostarczany toohello `.pull(query, queryname)` metody, a następnie synchronizacja przyrostowa jest tooreturn używanych tylko rekordy, które zostały utworzone lub zmienione w stosunku do ściągania hello ostatnia zakończona pomyślnie.

### <a name="handle-conflicts-during-offline-synchronization"></a>Obsługa konflikty podczas synchronizacji w trybie Offline

Jeśli wystąpi konflikt podczas `.push()` operacji `MobileServiceConflictException` jest generowany.   Element wystawiony serwera Hello jest osadzony w hello wyjątku i mogą zostać pobrane przez `.getItem()` na powitania wyjątku.  Dostosuj wypychania hello przez wywołanie hello następujących elementów w obiekcie MobileServiceSyncContext hello:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Gdy wszystkie konflikty zostały oznaczone jako mają, wywołaj `.push()` ponownie tooresolve hello wszystkie konflikty.

## <a name="custom-api"></a>Wywołaj niestandardowego interfejsu API

Niestandardowy interfejs API umożliwia toodefine niestandardowe punkty końcowe, które udostępniają funkcje serwera które nie mapy tooan insert, update, usuwania lub operacja odczytu. Przy użyciu niestandardowego interfejsu API, może mieć większą kontrolę nad wiadomości, w tym odczytywanie ustawienie nagłówki komunikatów HTTP i Definiowanie formatu treści wiadomości innych niż JSON.

Na kliencie z systemem Android należy wywołać hello **invokeApi** metody toocall hello niestandardowego interfejsu API punktu końcowego. Witaj poniższy przykład przedstawia sposób toocall interfejsu API punktu końcowego o nazwie **completeAll**, który zwraca klasę kolekcji o nazwie **MarkAllResult**.

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

Witaj **invokeApi** metoda jest wywoływana na powitania klienta, który wysyła ogłoszenie (POST) żądania toohello nowego niestandardowego interfejsu API. Witaj wynik zwracany przez hello niestandardowego interfejsu API jest wyświetlany w oknie dialogowym komunikatu, jak są błędy. Inne wersje **invokeApi** można opcjonalnie Wysyłanie obiektu w treści żądania hello, określ metodę hello HTTP i Wyślij parametry zapytania z żądaniem hello. Bez typu wersje **invokeApi** znajdują się również.

## <a name="authentication"></a>Dodaj aplikację tooyour uwierzytelniania

Samouczki już opisano szczegółowo sposób tooadd te funkcje.

Usługa aplikacji obsługuje [uwierzytelnianie użytkowników aplikacji](app-service-mobile-android-get-started-users.md) przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account, Twitter i Azure Active Directory. Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy. Umożliwia także tożsamości hello reguł autoryzacji tooimplement uwierzytelnionych użytkowników w sieci wewnętrznej bazy danych.

Obsługiwane są dwa przepływy uwierzytelniania: **serwera** przepływu i **klienta** przepływu. powitania serwera przepływu zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu sieci web dostawcy tożsamości hello.  Nie dodatkowe zestawy SDK są wymagane tooimplement serwera przepływ uwierzytelniania. Uwierzytelnianie serwera przepływu nie głęboką integrację hello urządzeń przenośnych i jest zalecane tylko dla dowód scenariuszy koncepcji.

powitania klienta przepływ umożliwia lepszą integrację z możliwości specyficznych dla urządzeń, takich jak logowanie jednokrotne zależy od udostępniane przez dostawcę tożsamości hello zestawów SDK.  Na przykład można zintegrować hello Facebook zestawu SDK aplikacji mobilnej.  powitania klienta mobilnego zamienia do aplikacji usługi Facebook hello i sprawdza z logowania jednokrotnego przed wymiany wstecz tooyour aplikacji mobilnej.

Cztery kroki są wymagane tooenable uwierzytelniania w aplikacji:

* Rejestrowanie aplikacji do uwierzytelniania przy użyciu dostawcy tożsamości.
* Skonfiguruj z wewnętrzną bazą danych z usługi aplikacji.
* Ogranicz użytkowników tooauthenticated uprawnienia tabeli tylko na powitania wewnętrznej bazy danych z usługi aplikacji.
* Dodaj aplikację tooyour kod uwierzytelniania.

Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy. Można również użyć hello identyfikator SID użytkownika uwierzytelnionego toomodify żądań.  Aby uzyskać więcej informacji, przejrzyj [Rozpoczynanie pracy z uwierzytelnianiem] i hello dokumentacji Porada zestawu SDK serwera.

### <a name="caching"></a>Uwierzytelniania: Przepływ serwera

Witaj następujący kod uruchamia proces logowania przepływu serwera przy użyciu dostawcy Google hello.  Ze względu na wymagania zabezpieczeń hello dostawcy Google hello jest wymagana dodatkowa konfiguracja:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Ponadto Dodaj powitania po klasie działania głównego — metoda toohello:

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

Hello `GOOGLE_LOGIN_REQUEST_CODE` zdefiniowane w głównym Twojego to działanie służy do hello `login()` — metoda i w obrębie hello `onActivityResult()` metody.  Można wybrać dowolny unikatowy numer, tak długo, jak hello sam numer jest używany w ramach hello `login()` — metoda i hello `onActivityResult()` metody.  Jeśli kod klienta hello jest abstrakcyjny karty service (jak pokazano wcześniej), należy wywołać hello odpowiednie metody hello usługi karty.

Należy również tooconfigure hello projektu dla customtabs.  Najpierw określ URL przekierowania.  Dodaj powitania po fragment zbyt`AndroidManifest.xml`:

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

Dodaj hello **redirectUriScheme** toohello `build.gradle` plików dla aplikacji:

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

Na koniec należy dodać `com.android.support:customtabs:23.0.1` toohello listę zależności w hello `build.gradle` pliku:

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

Uzyskać identyfikator hello hello zalogowanego użytkownika z **MobileServiceUser** przy użyciu hello **metodę getUserId** metody. Na przykład jak toocall prognoz toouse hello asynchroniczne logowania interfejsów API, zobacz [Rozpoczynanie pracy z uwierzytelnianiem].

> [!WARNING]
> Schemat adresów URL wymienionych Hello jest rozróżniana wielkość liter.  Upewnij się, że wszystkie wystąpienia `{url_scheme_of_you_app}` wielkość liter.

### <a name="caching"></a>Tokeny uwierzytelniania pamięci podręcznej

Buforowanie tokeny uwierzytelniania wymaga hello toostore identyfikator użytkownika i token uwierzytelniania lokalnie na powitania urządzenia. Witaj następnym uruchomieniu aplikacji hello sprawdzania hello pamięci podręcznej, a jeśli te wartości są obecne, możesz pominąć dziennika hello w procedurze i rehydrate powitania klienta przy użyciu tych danych. Jednak te dane są poufne i powinny być przechowywane, szyfrowane ze względów bezpieczeństwa w przypadku kradzieży hello telefonu.  Widać pełny przykład sposobu uwierzytelniania toocache tokenów w [pamięci podręcznej sekcji tokeny uwierzytelniania][7].

Podczas próby toouse wygasły token pojawi się *401 nieautoryzowane* odpowiedzi. Może obsługiwać błędy uwierzytelniania za pomocą filtrów.  Filtry przechwycić toohello żądań aplikacji usługi wewnętrznej bazy danych. Kod filtru Hello testów hello odpowiedzi 401, wyzwala hello procesu logowania i zostanie wznowiony hello żądania, który wygenerował hello 401.

### <a name="refresh"></a>Używaj tokenów odświeżania

token Hello zwracany przez usługi Azure App Service uwierzytelniania i autoryzacji ma zdefiniowany czas jedną godzinę.  Po tym okresie ponownego uwierzytelnienia użytkownika hello.  W przypadku tego samego tokenu hello z usługi Azure App Service Authentication przy użyciu długotrwałe token, który ma odebranych za pośrednictwem uwierzytelniania przepływu klienta, a następnie można ponownego uwierzytelnienia i autoryzacji.  Inny token usługi Azure App Service jest generowany nowy okres istnienia.

Można również zarejestrować hello toouse dostawcy tokenów odświeżania.  Token odświeżania nie zawsze jest dostępne.  Wymagana jest dodatkowa konfiguracja:

* Aby uzyskać **usługi Azure Active Directory**, skonfiguruj klucz tajny klienta na powitania aplikacji usługi Azure Active Directory.  Określ klucz tajny klienta hello hello Azure App Service, podczas konfigurowania uwierzytelniania usługi Azure Active Directory.  Podczas wywoływania metody `.login()`, Przekaż `response_type=code id_token` jako parametr:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Aby uzyskać **Google**, Przekaż hello `access_type=offline` jako parametr:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Aby uzyskać **Account Microsoft**, wybierz pozycję hello `wl.offline_access` zakresu.

Wywołanie toorefresh token, `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Najlepszym rozwiązaniem utworzyć filtr, który wykryje 401 odpowiedzi z serwera hello i próbuje toorefresh hello tokenu.

## <a name="log-in-with-client-flow-authentication"></a>Zaloguj się przy użyciu uwierzytelniania przepływu klienta

Witaj ogólny proces logowania się za pomocą klienta przepływ uwierzytelniania wygląda następująco:

* Konfigurowanie usługi Azure App Service uwierzytelniania i autoryzacji, jak w przypadku uwierzytelniania serwera przepływu.
* Integracja hello dostawcy uwierzytelniania zestawu SDK dla uwierzytelniania tooproduce tokenu dostępu.
* Wywołaj hello `.login()` metody w następujący sposób:

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

Zastąp hello `onSuccess()` metody z dowolnym kod ma toouse na pomyślnego logowania.  Witaj `{provider}` ciąg jest prawidłowym dostawcą: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, lub **twitter**.  Jeśli zaimplementowano niestandardowe uwierzytelnianie, można również użyć hello uwierzytelniania niestandardowego dostawcy tagu.

### <a name="adal"></a>Uwierzytelnianie użytkowników z hello Active Directory Authentication Library (ADAL)

Witaj Active Directory Authentication Library (ADAL) toosign użytkowników służy do aplikacji przy użyciu usługi Azure Active Directory. Przy użyciu identyfikatora logowania przepływu klienta jest często hello preferowane toousing `loginAsync()` metody, ponieważ zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.

1. Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD przez następujące hello [jak tooconfigure aplikacji usługi dla usługi Active Directory logowania] [ 22] samouczka. Upewnij się, że toocomplete hello opcjonalny krok rejestrowania aplikację native client.
2. Zainstaluj biblioteki ADAL, modyfikując Twojej hello tooinclude plik build.gradle następujące definicje:

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

1. Dodaj hello następującego kodu tooyour aplikacji, przez co hello następujące elementy zastępcze:

* Zastąp **INSERT urzędu tutaj** o nazwie hello hello dzierżawy, w którym są udostępniane aplikacji. https://login.microsoftonline.com/contoso.onmicrosoft.com powinna mieć ona Hello format.
* Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta powitania dla zaplecza aplikacji mobilnej. Identyfikator klienta hello można uzyskać z hello **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu hello.
* Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta hello skopiowany z hello aplikację native client.
* Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS. Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*.

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

## <a name="filters"></a>Dostosuj hello komunikacji klient-serwer

Witaj połączenie klienta jest zwykle podstawowe połączenie HTTP przy użyciu hello podstawowej biblioteki HTTP dostarczony wraz z hello zestawu SDK systemu Android.  Istnieje kilka przyczyn, dlaczego warto toochange który:

* Chcesz toouse alternatywny HTTP biblioteki tooadjust przekroczeń limitu czasu.
* Chcesz tooprovide pasek postępu.
* Chcesz tooadd z funkcji zarządzania toosupport interfejsu API niestandardowego nagłówka.
* Chcesz toointercept odpowiedzi nie powiodło się, aby zaimplementować ponowne uwierzytelnianie.
* Chcesz, aby usługa analiza tooan toolog wewnętrznej bazy danych żądania.

### <a name="using-an-alternate-http-library"></a>Za pomocą alternatywnej biblioteki HTTP

Wywołaj hello `.setAndroidHttpClientFactory()` metody natychmiast po utworzeniu odwołanie do klienta.  Na przykład tooset hello połączenia too60 liczba sekund limitu czasu (zamiast domyślnego hello 10 sekund):

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

### <a name="implement-a-progress-filter"></a>Implementuje filtr postępu

ODCIĘTA każde żądanie można zaimplementować zaimplementowanie `ServiceFilter`.  Na przykład następujące hello aktualizuje pasek postępu wstępnie utworzone:

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

Możesz dołączyć ten klient toohello filtru w następujący sposób:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Dostosowywanie nagłówki żądania

Użyj następujących hello `ServiceFilter` i Dołącz filtr hello w hello tak samo jak hello `ProgressFilter`:

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

### <a name="conversions"></a>Skonfiguruj automatyczne serializacji

Można określić strategii konwersji, która ma zastosowanie tooevery kolumny za pomocą hello [gson] [ 3] interfejsu API. Biblioteka klienta dla systemu Android Hello używa [gson] [ 3] tle hello tooserialize Java obiekty tooJSON danych przed wysłaniem danych hello tooAzure usługi aplikacji.  Witaj poniższy kod używa hello **setFieldNamingStrategy()** strategii hello tooset metody. W tym przykładzie spowoduje usunięcie hello początkowy znak ("m"), a następnie małe hello następny znak, dla każdej nazwy pola. Na przykład go spowoduje przekształcenie "mId" w "id".  Implementowanie potrzebę hello tooreduce strategii konwersji `SerializedName()` adnotacje w większości pól.

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

Ten kod musi zostać wykonana przed utworzeniem odwołanie klientów urządzeń przenośnych przy użyciu hello **MobileServiceClient**.

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
