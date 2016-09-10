# TextBoxBinding
A UWP project to show a bug in x:Bind for TextBox

The setup needs a textbox with two way binding to a property in the model using x:Bind. There is a sumbit button and a back button on the submitted page. The moment you wire a text changing event of the text box, the app crashes when we come back to the main page post submit.

Text box markup:

```xml
<TextBox x:Name="txt" Text="{x:Bind Model.FullName, Mode=TwoWay}" PlaceholderText="Enter name and Submit" />
```

Code behind:

```cs
public Model Model { get; } = (Application.Current as App).Model;

private void Button_Click(object sender, RoutedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;
    rootFrame.Navigate(typeof(SubmitPage));
}
```

The error condition when we wire a event in the MainPage constructor

```cs
public MainPage()
{
    this.InitializeComponent();

    // This is the line that causes a app crash.
    txt.TextChanging += Txt_TextChanging;
}
 

private void Txt_TextChanging(TextBox sender, TextBoxTextChangingEventArgs args)
{

}
```

Steps to reproduce the error when running app

* Type some text in the text box.
* Click submit button
* The app navigates to a new page which conatins a back button.
* Click the back button to cause app crash


