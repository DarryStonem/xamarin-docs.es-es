---
title: Autocompletar
ms.topic: article
ms.prod: xamarin
ms.assetid: D4C8CA49-8369-35B7-798D-B147FDC24185
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/06/2018
ms.openlocfilehash: f4118881272bb605607d528007064ada561cf7fc
ms.sourcegitcommit: 30055c534d9caf5dffcfdeafd6f08e666fb870a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2018
---
# <a name="auto-complete"></a>Autocompletar


## <a name="overview"></a>Información general

Para crear un widget de entrada de texto que se proporciona sugerencias de Autocompletar, use la [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget. Sugerencias se reciben de una colección de cadenas asociadas con el widget a través de un [ `ArrayAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/).

En este tutorial, aprenderá a crear un [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget que se proporciona sugerencias para un nombre de país.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:padding="5dp">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Country" />
    <AutoCompleteTextView android:id="@+id/autocomplete_country"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:layout_marginLeft="5dp"/>
</LinearLayout>
```

El [ `TextView` ](https://developer.xamarin.com/api/type/Android.Widget.TextView/) es una etiqueta que presenta la [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget.


## <a name="tutorial"></a>Tutorial

Inicie un nuevo proyecto denominado *HelloAutoComplete*.

Crear un archivo XML denominado `list_item.xml` y guardarlo en el interior del **recursos/diseño** carpeta. Establecer la acción de compilación de este archivo a `AndroidResource`. Edite el archivo debe ser similar a esto:

```xml
<?xml version="1.0" encoding="utf-8"?>

<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:padding="10dp"
    android:textSize="16sp"
    android:textColor="#000">
</TextView>
```

Este archivo define una sencilla [ `TextView` ](https://developer.xamarin.com/api/type/Android.Widget.TextView/) que se usará para cada elemento que aparece en la lista de sugerencias.

Abra **Resources/Layout/Main.axml** e inserte lo siguiente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:padding="5dp">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Country" />
    <AutoCompleteTextView android:id="@+id/autocomplete_country"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:layout_marginLeft="5dp"/>
</LinearLayout>
```

Abra **MainActivity.cs** e inserte el siguiente código para el [ `OnCreate()` ](https://developer.xamarin.com/api/member/Android.App.Activity.OnCreate/(Android.OS.Bundle)) método:

```csharp
protected override void OnCreate (Bundle bundle)
{
    base.OnCreate (bundle);

    // Set our view from the "Main" layout resource
    SetContentView (Resource.Layout.Main);

    AutoCompleteTextView textView = FindViewById<AutoCompleteTextView> (Resource.Id.autocomplete_country);
    var adapter = new ArrayAdapter<String> (this, Resource.Layout.list_item, COUNTRIES);

    textView.Adapter = adapter;
}
```

Después de la vista de contenido se establece en el `main.xml` diseño, el [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget se captura desde el diseño con [ `FindViewById` ](https://developer.xamarin.com/api/member/Android.App.Activity.FindViewById/). Un nuevo [ `ArrayAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/) , a continuación, se inicializa para enlazar la `list_item.xml` diseño para cada elemento de lista en la `COUNTRIES` matriz de cadenas (definido en el paso siguiente). Por último, `SetAdapter()` se llama para asociar el [ `ArrayAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/) con el [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget para que la matriz de cadenas llenará la lista de sugerencias.

Dentro de la `MainActivity` clase, agregue la matriz de cadenas:

```csharp
static string[] COUNTRIES = new string[] {
  "Afghanistan", "Albania", "Algeria", "American Samoa", "Andorra",
  "Angola", "Anguilla", "Antarctica", "Antigua and Barbuda", "Argentina",
  "Armenia", "Aruba", "Australia", "Austria", "Azerbaijan",
  "Bahrain", "Bangladesh", "Barbados", "Belarus", "Belgium",
  "Belize", "Benin", "Bermuda", "Bhutan", "Bolivia",
  "Bosnia and Herzegovina", "Botswana", "Bouvet Island", "Brazil", "British Indian Ocean Territory",
  "British Virgin Islands", "Brunei", "Bulgaria", "Burkina Faso", "Burundi",
  "Cote d'Ivoire", "Cambodia", "Cameroon", "Canada", "Cape Verde",
  "Cayman Islands", "Central African Republic", "Chad", "Chile", "China",
  "Christmas Island", "Cocos (Keeling) Islands", "Colombia", "Comoros", "Congo",
  "Cook Islands", "Costa Rica", "Croatia", "Cuba", "Cyprus", "Czech Republic",
  "Democratic Republic of the Congo", "Denmark", "Djibouti", "Dominica", "Dominican Republic",
  "East Timor", "Ecuador", "Egypt", "El Salvador", "Equatorial Guinea", "Eritrea",
  "Estonia", "Ethiopia", "Faeroe Islands", "Falkland Islands", "Fiji", "Finland",
  "Former Yugoslav Republic of Macedonia", "France", "French Guiana", "French Polynesia",
  "French Southern Territories", "Gabon", "Georgia", "Germany", "Ghana", "Gibraltar",
  "Greece", "Greenland", "Grenada", "Guadeloupe", "Guam", "Guatemala", "Guinea", "Guinea-Bissau",
  "Guyana", "Haiti", "Heard Island and McDonald Islands", "Honduras", "Hong Kong", "Hungary",
  "Iceland", "India", "Indonesia", "Iran", "Iraq", "Ireland", "Israel", "Italy", "Jamaica",
  "Japan", "Jordan", "Kazakhstan", "Kenya", "Kiribati", "Kuwait", "Kyrgyzstan", "Laos",
  "Latvia", "Lebanon", "Lesotho", "Liberia", "Libya", "Liechtenstein", "Lithuania", "Luxembourg",
  "Macau", "Madagascar", "Malawi", "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands",
  "Martinique", "Mauritania", "Mauritius", "Mayotte", "Mexico", "Micronesia", "Moldova",
  "Monaco", "Mongolia", "Montserrat", "Morocco", "Mozambique", "Myanmar", "Namibia",
  "Nauru", "Nepal", "Netherlands", "Netherlands Antilles", "New Caledonia", "New Zealand",
  "Nicaragua", "Niger", "Nigeria", "Niue", "Norfolk Island", "North Korea", "Northern Marianas",
  "Norway", "Oman", "Pakistan", "Palau", "Panama", "Papua New Guinea", "Paraguay", "Peru",
  "Philippines", "Pitcairn Islands", "Poland", "Portugal", "Puerto Rico", "Qatar",
  "Reunion", "Romania", "Russia", "Rwanda", "Sqo Tome and Principe", "Saint Helena",
  "Saint Kitts and Nevis", "Saint Lucia", "Saint Pierre and Miquelon",
  "Saint Vincent and the Grenadines", "Samoa", "San Marino", "Saudi Arabia", "Senegal",
  "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands",
  "Somalia", "South Africa", "South Georgia and the South Sandwich Islands", "South Korea",
  "Spain", "Sri Lanka", "Sudan", "Suriname", "Svalbard and Jan Mayen", "Swaziland", "Sweden",
  "Switzerland", "Syria", "Taiwan", "Tajikistan", "Tanzania", "Thailand", "The Bahamas",
  "The Gambia", "Togo", "Tokelau", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey",
  "Turkmenistan", "Turks and Caicos Islands", "Tuvalu", "Virgin Islands", "Uganda",
  "Ukraine", "United Arab Emirates", "United Kingdom",
  "United States", "United States Minor Outlying Islands", "Uruguay", "Uzbekistan",
  "Vanuatu", "Vatican City", "Venezuela", "Vietnam", "Wallis and Futuna", "Western Sahara",
  "Yemen", "Yugoslavia", "Zambia", "Zimbabwe"
};
```

Esta es la lista de sugerencias que se proporcionará en una lista desplegable cuando el usuario escribe en el [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget.

Ejecute la aplicación. A medida que escribe, debería ver algo parecido a esto:

[![Pantalla de Autocompletar en el ejemplo se presenta los nombres que contienen "ca"](auto-complete-images/helloautocomplete.png)](auto-complete-images/helloautocomplete.png#lightbox)



## <a name="more-information"></a>Más información

Tenga en cuenta que no es una práctica de diseño recomendado porque el código de aplicación debe centrarse en el comportamiento, no contenido mediante una matriz de cadenas codificadas de forma rígida. Contenido de la aplicación, como cadenas debe ser externalizado desde el código para realizar modificaciones en el contenido sea más fácil y facilitar la localización del contenido. Las cadenas codificadas de forma rígida se utilizan en este tutorial sólo para facilitar y centrarse en el [ `AutoCompleteTextView` ](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/) widget. En su lugar, la aplicación debe declarar estas matrices de cadena en un archivo XML. Esto puede hacerse con un `<string-array>` recursos en el proyecto `res/values/strings.xml` archivo. Por ejemplo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="countries_array">
        <item>Bahrain</item>
        <item>Bangladesh</item>
        <item>Barbados</item>
        <item>Belarus</item>
        <item>Belgium</item>
        <item>Belize</item>
        <item>Benin</item>
    </string-array>
</resources>
```

Para usar estas cadenas de recursos para la [ `ArrayAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/), sustituya el original [ `ArrayAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/) línea constructor con lo siguiente:

```csharp
string[] countries = Resources.GetStringArray (Resource.array.countries_array);
var adapter = new ArrayAdapter<String> (this, Resource.layout.list_item, countries);
```


### <a name="references"></a>Referencias

-   [`ArrayAdapter`](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/)
-   [`AutoCompleteTextView`](https://developer.xamarin.com/api/type/Android.Widget.AutoCompleteTextView/)

*Algunas partes de esta página son las modificaciones que se basa en el trabajo creado y comparten la Android Open Source Project y usarse de acuerdo con los términos que se describe en el* 
 [ *licencia de atribución 2.5 de Creative Commons* ](http://creativecommons.org/licenses/by/2.5/) *. Este tutorial se basa en el* 
 [ *Android automáticamente todo el tutorial*](http://developer.android.com/resources/tutorials/views/hello-autocomplete.html)
*.*
