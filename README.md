<div align="center">

## Create a form bigger than the screen\!


</div>

### Description

The primary focus here is to allow you to display forms that are larger than the screen can show. Need an 8½" x 11" Form? NO Problem!The size used in this example is 8½" x 11", but it could just as easily be landscape, envelope, or any needed size.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[VB Tips and Source Code](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/vb-tips-and-source-code.md)
**Level**          |Unknown
**User Rating**    |4.8 (24 globes from 5 users)
**Compatibility**  |VB 3\.0, VB 4\.0 \(16\-bit\), VB 4\.0 \(32\-bit\), VB 5\.0, VB 6\.0
**Category**       |[Custom Controls/ Forms/  Menus](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/custom-controls-forms-menus__1-4.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/vb-tips-and-source-code-create-a-form-bigger-than-the-screen__1-153/archive/master.zip)





### Source Code

```
Place a Horizontal Scrollbar on the form (doesn't matter where) and set its properties as follows:
   Height     =  300
   LargeChange   =  900
   Name      = HScroll
   SmallChange   =  30
These properties do not need to be identical to mine, but will serve as a good common ground starting point. You can always modify them to suit your needs and taste later.
Now, let's place a Vertical Scrollbar on the form (doesn't matter where) and set its properties as follows:
   LargeChange   =  900
   Name      = VScroll
   SmallChange   =  30
   Width      =  300
Now, for the magic. Place a PictureBox on your form and set the following properties for it. The PictureBox will serve as our container for all controls and graphics that need to be placed on the virtual form.
   BackColor    =  &H00FFFFFF&
   Height     =  15900
   Name      = PicBox
   Width      =  11640
There is one last control that we need to place on the virtual form. However, this control is not placed directly onto the form but onto the picture box. It is a label that will serve as a filler to cover up the gap left between the two scrollbars in the lower right hand corner. Click on the PictureBox to select it, then double click the Label control on the VB Toolbox. Make sure that the label is the same color as your scrollbars. Then set its properties as follows:
   Height     =  300
   Name      = lblFiller
   Width      =  300
From this point on, all of the control that are placed on the virtual form (the picturebox) are solely for our own visual evidence that the form does indeed move. Place any controls you wish and set their properties as you wish on the form. (The downloadable project has already placed several controls on the picture box for you.)
Let's start our Coding process by writing a routine to line everything up the way it should be. We need to place the scrollbars where they should go, make their dimensions match that of the form, and also position the lblFiller label properly. I have called this procedure AlignScrollBars(). This procedure needs to be placed in your General Decalrations section. The code looks like this:
Sub AlignScrollBars()
  ' Resize the scrollbars
  HScroll.Width = Me.ScaleWidth - lblFiller.Width
  VScroll.Height = Me.ScaleHeight - lblFiller.Height
  ' Reposition the scrollbars
  HScroll.Left = 0: HScroll.Top = Me.ScaleHeight - HScroll.Height
  VScroll.Top = 0: VScroll.Left = Me.ScaleWidth - VScroll.Width
  ' Redimension the scrollbar parameters
  HScroll.Max = PicBox.Width - Me.ScaleWidth
  VScroll.Max = PicBox.Height - Me.ScaleHeight
  ' Reposition the PictureBox
  PicBox.Top = (-1 * VScroll)
  PicBox.Left = (-1 * HScroll)
  ' Reposition the Picturebox label by scrollbars
  lblFiller.Top = VScroll.Height + VScroll - 30
  lblFiller.Left = HScroll.Width + HScroll - 30
  UpdateDisplay
End Sub
Note the call to UpdateDisplay. That procedure is just for the fun of it. I have used it to create some text and a graphic on the form at run time. This is what the procedure looks like.
For VB4:
Sub UpdateDisplay()
  ' Place text on the PictureBox
  PicBox.AutoRedraw = True
  Dim PictureBoxText As String
  PictureBoxText = "Virtual Form - 8½ x 11 size"
  With PicBox
    .Font = "Arial"
    .FontSize = 14
    .FontBold = True
    .FontItalic = True
    .CurrentX = (PicBox.Width - PicBox.TextWidth(PictureBoxText)) / 2
    .CurrentY = 0
  End With
  PicBox.Print PictureBoxText
  ' Graphics can be drawn on the virtual form at run time
  PicBox.Line (100, 100)-(500, 500), , B
End Sub
For VB3: (since the WITH construct is only available in VB4.)
Sub UpdateDisplay()
  ' Place text on the PictureBox
  PicBox.AutoRedraw = True
  Dim PictureBoxText As String
  PictureBoxText = "Virtual Form - 8½ x 11 size"
  PicBox.Font = "Arial"
  PicBox.FontSize = 14
  PicBox.FontBold = True
  PicBox.FontItalic = True
  PicBox.CurrentX = (PicBox.Width - PicBox.TextWidth(PictureBoxText)) / 2
  PicBox.CurrentY = 0
  PicBox.Print PictureBoxText
  ' Graphics can be drawn on the virtual form at run time
  PicBox.Line (100, 100)-(500, 500), , B
End Sub
At this point, there are only three procedures left for us to code. We need to be able to realign the controls (scrollbars, etc) each time the scrollbars are clicked and each time the form is resized. I have written these three procedures like this: (Of course in VB3 you will want to remove the Private keyword from the SUB line).
Private Sub Form_Resize()
  AlignScrollBars
End Sub
Private Sub HScroll_Change()
  AlignScrollBars
End Sub
Private Sub VScroll_Change()
  AlignScrollBars
End Sub
Now, save your project and run the thing. If you have placed additional controls on the picturebox during design time, you should be able to see them float across the screen as your scroll around. Keep in mind that during design time, you can drag the picturebox around to work with the sections that are not visible within the form. The code will line everything back up so you don't even have to clean up behind yourself.
```

