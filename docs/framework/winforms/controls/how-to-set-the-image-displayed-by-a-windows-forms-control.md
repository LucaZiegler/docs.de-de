---
title: 'Gewusst wie: Festlegen des durch ein Windows Forms-Steuerelement angezeigten Bildes'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Button control [Windows Forms], images
- Windows Forms controls, images
- controls [Windows Forms], images
- images [Windows Forms], Windows Forms controls
- examples [Windows Forms], controls
ms.assetid: 9445af8f-4f62-48b0-a3f6-068058964b9f
ms.openlocfilehash: 4870f9e2acc48a90e1e2193d514926fedee05f61
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-set-the-image-displayed-by-a-windows-forms-control"></a>Gewusst wie: Festlegen des durch ein Windows Forms-Steuerelement angezeigten Bildes
Einige Windows Forms-Steuerelemente können Bilder anzuzeigen. Diese Bilder können Symbole, die Erläuterung des Zwecks des Steuerelements, wie z. B. ein Diskettensymbol auf eine Schaltfläche, werden die **speichern** Befehl. Alternativ kann die Symbole Hintergrundbilder zum Steuern der Darstellung und das gewünschte Verhalten.  
  
### <a name="to-set-the-image-displayed-by-a-control"></a>Das von einem Steuerelement angezeigte Bild festlegen  
  
1.  Legen Sie das Steuerelement `Image` oder `BackgroundImage` Eigenschaft, um ein Objekt vom Typ <xref:System.Drawing.Image>. Im Allgemeinen, laden Sie das Bild aus einer Datei mithilfe der <xref:System.Drawing.Image.FromFile%2A> Methode.  
  
     Im folgenden Codebeispiel legen der Pfad für der Speicherort des Bilds wird die **eigene Bilder** Ordner. Die meisten Computer das Windows-Betriebssystem ausgeführt wird, werden dieses Verzeichnis enthalten. Außerdem können Benutzer mit minimalen problemlos die Anwendung auszuführen. Das folgende Codebeispiel erfordert, dass Sie bereits ein Formular mit einem <xref:System.Windows.Forms.PictureBox> ein Steuerelement hinzugefügt wurde.  
  
    ```vb  
    ' Replace the image named below  
    ' with an icon of your own choosing.  
    PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.MyPictures) _  
       & "\Image.gif")  
    ```  
  
    ```csharp  
    // Replace the image named below  
    // with an icon of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    pictureBox1.Image = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.MyPictures)  
       + @"\Image.gif");  
    ```  
  
    ```cpp  
    // Replace the image named below  
    // with an icon of your own choosing.  
    pictureBox1->Image = Image::FromFile(String::Concat  
       (System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::MyPictures),  
       "\\Image.gif"));  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Drawing.Image.FromFile%2A>  
 <xref:System.Drawing.Image>  
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>
