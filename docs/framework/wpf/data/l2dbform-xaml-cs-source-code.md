---
title: Kod źródłowy L2DBForm.xaml.cs
ms.date: 10/22/2019
ms.topic: sample
ms.openlocfilehash: 882699a76eab3c291cd92c298287bc5d28fb08e1
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/25/2019
ms.locfileid: "72920861"
---
# <a name="l2dbformxamlcs-source-code"></a>Kod źródłowy L2DBForm.xaml.cs

Ta strona zawiera zawartość i Opis kodu C# źródłowego w pliku *L2DBForm.XAML.cs*. Klasa częściowa L2XDBForm znajdująca się w tym pliku może zostać podzielona na trzy sekcje logiczne: elementy członkowskie danych i przycisk `OnRemove` i `OnAddBook` kliknij pozycję Programy obsługi zdarzeń.

## <a name="data-members"></a>Elementy członkowskie danych

Dwa prywatne elementy członkowskie danych są używane do kojarzenia tej klasy z zasobami okna używanymi w *kod źródłowy L2DBForm. XAML*.

- Zmienna przestrzeni nazw `myBooks` została zainicjowana, aby `"http://www.mybooks.com"`.

- `bookList` elementu członkowskiego jest inicjowana w konstruktorze do ciągu CDATA w *kod źródłowy L2DBForm. XAML* z następującym wierszem:

    ```csharp
    bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
    ```

## <a name="onaddbook-event-handler"></a>Procedura obsługi zdarzeń OnAddBook

Ta metoda zawiera trzy następujące instrukcje:

- Pierwsza Instrukcja warunkowa służy do sprawdzania poprawności danych wejściowych.

- Druga instrukcja tworzy nowe <xref:System.Xml.Linq.XElement> z wartości ciągów wprowadzonych przez użytkownika w sekcji **Dodaj nowy** interfejs użytkownika książki (UI).

- Ostatnia instrukcja dodaje nowy element książki do dostawcy danych w *kod źródłowy L2DBForm. XAML*. W związku z tym dynamiczne powiązanie danych automatycznie zaktualizuje interfejs użytkownika przy użyciu tego nowego elementu; nie jest wymagany żaden dodatkowy kod dostarczony przez użytkownika.

## <a name="onremove-event-handler"></a>Procedura obsługi zdarzeń OnRemove

Procedura obsługi `OnRemove` jest bardziej skomplikowana niż obsługa `OnAddBook` z dwóch przyczyn. Po pierwsze, ponieważ nieprzetworzony kod XML zawiera zachowany biały znak, należy również usunąć pasujące znaki nowego wiersza z wpisem książki. Po drugie, jako wygoda, wybór, który został usunięty z usuniętego elementu, jest resetowany do poprzedniej z nich na liście.

Jednak podstawowe zadania usuwania wybranego elementu księgi są wykonywane tylko przez dwie instrukcje:

- Najpierw zostanie pobrany element Book skojarzony z aktualnie wybranym elementem w polu listy:

    ```csharp
    XElement selBook = (XElement)lbBooks.SelectedItem;
    ```

- Następnie ten element zostanie usunięty z dostawcy danych:

    ```csharp
    selBook.Remove();
    ```

Po ponownym rozwiązaniu danych dynamicznych gwarantuje, że interfejs użytkownika programu jest automatycznie aktualizowany.

## <a name="example"></a>Przykład

### <a name="code"></a>Kod

```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Input;
using System.Xml;
using System.Xml.Linq;

namespace LinqToXmlDataBinding {
    /// <summary>
    /// Interaction logic for L2XDBForm.xaml
    /// </summary>

    public partial class L2XDBForm : System.Windows.Window
    {
        XNamespace mybooks = "http://www.mybooks.com";
        XElement bookList;

        public L2XDBForm()
        {
            InitializeComponent();
            bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
        }

        void OnRemoveBook(object sender, EventArgs e)
        {
            int index = lbBooks.SelectedIndex;
            if (index < 0) return;

            XElement selBook = (XElement)lbBooks.SelectedItem;
            //Get next node before removing element.
            XNode nextNode = selBook.NextNode;
            selBook.Remove();

            //Remove any matching newline node.
            if (nextNode != null && nextNode.ToString().Trim().Equals(""))
            { nextNode.Remove(); }

            //Set selected item.
            if (lbBooks.Items.Count > 0)
            {  lbBooks.SelectedItem = lbBooks.Items[index > 0 ? index - 1 : 0]; }
        }

        void OnAddBook(object sender, EventArgs e)
        {
            if (String.IsNullOrEmpty(tbAddID.Text) ||
                String.IsNullOrEmpty(tbAddValue.Text))
            {
                MessageBox.Show("Please supply both a Book ID and a Value!", "Entry Error!");
                return;
            }
            XElement newBook = new XElement(
                                mybooks + "book",
                                new XAttribute("id", tbAddID.Text),
                                tbAddValue.Text);
            bookList.Add("  ", newBook, "\r\n");
        }
    }
}
```

### <a name="comments"></a>Komentarze

Dla skojarzonego źródła XAML dla tych programów obsługi zobacz [kod źródłowy kod źródłowy L2DBForm. XAML](l2dbform-xaml-source-code.md).

## <a name="see-also"></a>Zobacz także

- [Przewodnik: elementu LinqToXmlDataBinding — przykład](linq-to-xml-data-binding-sample.md)
- [Kod źródłowy L2DBForm.xaml](l2dbform-xaml-source-code.md)
