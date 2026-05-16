# neXt Window Management System (XWMS)

**neXt Window Management System** is a lightweight, high-performance window management library for VB.NET. It enables borderless WinForms applications to behave like modern Windows 11/10 windows, featuring Aero-Snap functionality, quadrant snapping, and asynchronous resize animations.

---

## Features

*  **Advanced Aero-Snap**: Drag windows to edges or corners to snap them into 50% or 25% screen segments.
*  **Async Animation Engine**: Smoothly transitions window bounds using an internal asynchronous system for a premium UI feel.
*  **Universal Dragging**: Turn any UI element (Panels, Labels, PictureBoxes) into a functional drag handle for your form.
*  **Smart Un-Snap**: Pulling a maximized or snapped window automatically restores it to its original dimensions.
*  **Multi-Quadrant Support**: Supports Top-Left, Top-Right, Bottom-Left, and Bottom-Right corner snapping for efficient screen organization.

---

## Integration Guide

### 1. Add Reference
Simply add the `neXt Window Managment System` DLL as a reference to your project solution.

### 2. Setup
To use the system, you initialize the manager within your Form and register the specific controls that should handle the dragging and snapping logic. 

### 3. Recommended Form Settings
For the best visual experience, the following settings are recommended in the Visual Studio Property Grid:
* **FormBorderStyle**: Set to `None`.
* **DoubleBuffered**: Set to `True` to eliminate flickering during transitions.

---

## Snap Layouts & Zones

The system detects the cursor position relative to the screen's working area (respecting the taskbar) to trigger the following layouts:



| Trigger Zone | Snap Result | Description |
| :--- | :--- | :--- |
| **Top Edge** | **Full Maximize** | Fills the entire working area. |
| **Left/Right Edges** | **Vertical Half** | Snaps to 50% width and 100% height. |
| **Top Corners** | **Quadrant Snap** | Snaps to 50% width and 50% height in corners. |
| **Bottom Edge** | **Bottom Half** | Snaps to 100% width and 50% height at the bottom. |
| **Bottom Corners** | **Quadrant Snap** | Snaps to 50% width and 50% height in bottom corners. |

---

##  API Documentation

### Core Methods
* **AddControl**: Attaches the snap and drag logic to a specific UI element (e.g., a Header Panel).
* **MaximizeFull**: Animates the form to fill the entire working area of the current monitor.
* **OriginalSize**: Returns the form to its defined default dimensions and centers it.
* **SnapToLeft / SnapToRight**: Manually triggers vertical half-screen snaps via code.
* **SnapToLeftTop / SnapToRightTop**: Triggers 25% quadrant snaps.
* **SnapToBottomHalf**: Snaps the window to the lower horizontal half of the screen.

### Configuration Properties
* **DefaultWidth**: The width the window returns to when un-snapping.
* **DefaultHeight**: The height the window returns to when un-snapping.
* **_isMaxed**: A boolean status indicating if the window is currently in a snapped or maximized state.

---

##  Technical Requirements
* **Target Framework**: .NET 6.0+
* **OS**: Windows (Utilizes `user32.dll` for native window messaging).
* **Environment**: Compatible with all WinForms-supported development environments.

---

## Current Updates

### XenDesk Mode

The XenDesk mode allows it to make the library compatible with the normal Windows shell, because otherwise it was previously only for XenDesk and the scaling did not correspond to that of windows. Currently, an extended "Real-time workspace calculation and scaling" is being created so that the Windows shell elements can also be adopted (design phase).

## Tool Window Mode

The Tool Window Mode replaces the Windows Native implementation and allows you to create your own tool Windows with your own design (see [Compressed Map Data Tool](https://github.com/miyumelu/compressed-map-data) tool as an example). The first rollout is here, but it may be that some functions may be missing or incorrect due to the weak architecture.

## Resizable Window

Now you can use the right corner below to change the size.

### Forced Edges

The function has been installed, but the option to turn it off is still missing. This one will come soon.

### Dictionary Communication Layer

With newer features, there are also changeable settings that need to be secured elsewhere. Because of this, the DCL is also used here.

**Information**: The Dictionary Communication Layer is not a separate library but an in-house production for each library. More information about DCL can be found in the MaidNVI book.

## Issues

- I am aware that because of an exception, the XWMS can result in a crash of an app or a Black Screen of Death. I am currently trying to trace back the issue. For now, using it with .NET 9.0 or older seems to be the only fix.

- I realized that late, but the library name is broken. Managment instead of Management. I forgot an E... I'll try to rebuild it with a corrected name (or just delay it to the creation of a newer version of it)

## Rebuild

A new construction of the library is planned.

Each library is now merged with Melumetronics to form a SLCI (Simplified Library Collection Interface). MaidNVI is therefore only for legacy systems.

---

##  Example Usage

    Imports System.Drawing
    Imports neXt_Window_Managment_System

    Public Class MainForm
        Private xwms As Window
        
        Private Sub MainForm_Load(sender As Object, e As EventArgs) Handles MyBase.Load
            xwms = New Window(Me)
            xwms.AddControl(drag_panel)
            xwms.AddControl(name_label)
            xmws.SetToolWindowMode(False)
            xmws.SetXenDeskMode(False)
            xmws.ForcedEdges(True)
            xmws.Roundedcorners(20)
            xwns.ResizerResizable()
        End Sub
        
        Private Sub btnMaximize_Click(sender As Object, e As EventArgs) Handles btnMaximize.Click
            If xwms._isMaxed Then
                xwms.OriginalSize()
            Else
                xwms.MaximizeFull()
            End If
        End Sub
    End Class
