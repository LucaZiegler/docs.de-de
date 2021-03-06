---
title: 'Vorgehensweise: Lesen und Schreiben eines codierten Dokuments (C#)'
ms.date: 07/20/2015
ms.assetid: 84f64e71-39a6-42c6-ad68-f052bb158a03
ms.openlocfilehash: 9fc6a7beaa4a7b9de21961e1095dd41fe2e407dd
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-read-and-write-an-encoded-document-c"></a>Vorgehensweise: Lesen und Schreiben eines codierten Dokuments (C#)
Fügen Sie zum Erstellen eines codierten XML-Dokuments der XML-Struktur eine <xref:System.Xml.Linq.XDeclaration> hinzu, die die Codierung auf den gewünschten Codeseitennamen festlegt.  
  
 Jeder von <xref:System.Text.Encoding.WebName%2A> zurückgegebene Wert ist ein gültiger Wert.  
  
 Beim Lesen eines codierten Dokuments wird die <xref:System.Xml.Linq.XDeclaration.Encoding%2A>-Eigenschaft auf den Codeseitennamen festgelegt.  
  
 Wenn Sie die <xref:System.Xml.Linq.XDeclaration.Encoding%2A> auf einen gültigen Codeseitennamen festgelegt haben, verwendet [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] zum Serialisieren die angegebene Codierung.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel erstellt zwei Dokumente: eines mit UTF-8-Codierung und eines mit UTF-16-Codierung. Anschließend werden die Dokumente geladen, und die Codierung wird auf der Konsole ausgegeben.  
  
```csharp  
Console.WriteLine("Creating a document with utf-8 encoding");  
XDocument encodedDoc8 = new XDocument(  
    new XDeclaration("1.0", "utf-8", "yes"),  
    new XElement("Root", "Content")  
);  
encodedDoc8.Save("EncodedUtf8.xml");  
Console.WriteLine("Encoding is:{0}", encodedDoc8.Declaration.Encoding);  
Console.WriteLine();  
  
Console.WriteLine("Creating a document with utf-16 encoding");  
XDocument encodedDoc16 = new XDocument(  
    new XDeclaration("1.0", "utf-16", "yes"),  
    new XElement("Root", "Content")  
);  
encodedDoc16.Save("EncodedUtf16.xml");  
Console.WriteLine("Encoding is:{0}", encodedDoc16.Declaration.Encoding);  
Console.WriteLine();  
  
XDocument newDoc8 = XDocument.Load("EncodedUtf8.xml");  
Console.WriteLine("Encoded document:");  
Console.WriteLine(File.ReadAllText("EncodedUtf8.xml"));  
Console.WriteLine();  
Console.WriteLine("Encoding of loaded document is:{0}", newDoc8.Declaration.Encoding);  
Console.WriteLine();  
  
XDocument newDoc16 = XDocument.Load("EncodedUtf16.xml");  
Console.WriteLine("Encoded document:");  
Console.WriteLine(File.ReadAllText("EncodedUtf16.xml"));  
Console.WriteLine();  
Console.WriteLine("Encoding of loaded document is:{0}", newDoc16.Declaration.Encoding);  
```  
  
 Dieses Beispiel erzeugt die folgende Ausgabe:  
  
```  
Creating a document with utf-8 encoding  
Encoding is:utf-8  
  
Creating a document with utf-16 encoding  
Encoding is:utf-16  
  
Encoded document:  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root>Content</Root>  
  
Encoding of loaded document is:utf-8  
  
Encoded document:  
<?xml version="1.0" encoding="utf-16" standalone="yes"?>  
<Root>Content</Root>  
  
Encoding of loaded document is:utf-16  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Xml.Linq.XDeclaration.Encoding%2A?displayProperty=nameWithType>  
 [Advanced LINQ to XML Programming (C#) (Erweiterte LINQ to XML-Programmierung (C#))](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
